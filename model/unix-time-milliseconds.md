# UNIX Time \(Milliseconds\) 사용하기

## ActiveRecord의 타임스탬프

루비를 사용하면서 가장 놀랐던 점은 기본 타임스탬프를 `YYYY-MM-DD HH:mm:SS +0000` 형식으로 다룬다는 것이다.

일반적으로 다루는 UNIX Time\(Epoch 기준\)이나 ISO8601 스타일과 차이를 보인다.

루비는 시간을 63bit의 Signed Int로 다루기 때문에 실제로는 나노초 단위의 정밀도로 값을 저장하지만 어처구니 없게도 `#to_i()`를 호출하면 초 단위의 정밀도로 잘려나간 값을 반환한다. \(정말이지 이해할 수 없다\)

루비 온 레일즈는 한 술 더 떠서 타임스탬프를 DB에 저장할 때 컬럼 타입에 따라 `YYYY-MM-DD HH:mm:SS` 형식 문자열을 저장하거나 `to_i` 의 반환 값을 저장하는 기행을 보여준다.

따라서 컬럼타입을 `datetime`으로 저장하건 `bigint`로 저장하건 간에 초 이하의 정밀도를 지원할 수 없고 타임존 정보도 남지 않는다.

이 상황을 무마해서 UNIX Time을 기본으로 사용하고 싶다면 두 가지 정도의 작업이 필요하다. `config/initializers`에 파일을 만들자.

## Ruby 시간 객체 \#to\_i\(\) 정밀도 보정하기

```ruby
class Time
   def to_ms
     (to_f * 1000).round
   end
   
   def to_i
     to_ms
   end
end
```

이 코드는 `Time` 객체의 `to_i` 반환 정밀도를 밀리세컨드로 보정한다.

전역 오염에 의한 알 수 없는 오류가 걱정된다면 `ActiveRecord::Timestamp` 모듈로 스코프를 조정하거나 필요한 부분에 일일히 `to_ms`를 써주어도 되지만,

귀찮으니 전역에 적용하도록 하자. 일단 적어도 루비 온 레일즈와 관련 잼들에서는 문제가 없음을 확인하였다.

## ActiveRecord 타임스탬프의 타입 변경하기

```ruby
create_table :users |t| do
  t.bigint :created_at, null: false
  t.bigint :updated_at, null: false
end
```

타임스탬프 기능에서 중요한 것은 어차피 `created_at`, `created_on`, `updated_at`, `updated_on` 이라는 컬럼 이름이기에 위와 같이 생성 시 타입만 변경하는 것으로도 잘 동작한다. \(포맷 스트링을 찍는 대신 암묵적으로 `#to_i()`를 사용한다.\)

다만 이게 귀찮고 이전처럼 `t.timestamps`만 사용하고 싶다면 아래와 같이 initializer에 코드를 추가한다.

```ruby
module ActiveRecord
  module ConnectionAdapters 
    class TableDefinition
      def timestamps(**options)
        options[:null] = false if options[:null].nil?
        column(:created_at, :bigint, options)
        column(:updated_at, :bigint, options)
      end
    end
  end
end
```



이제 우리 코드베이스는 2038년이 지나도 안전하다.

