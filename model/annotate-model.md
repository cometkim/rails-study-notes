# Annotate Model

## 소개

모델 관련 파일에 테이블 구조에 대한 주석을 생성해주는 유용한 잼이다.

* [Gem](https://rubygems.org/gems/annotate)
* [Source](https://github.com/ctran/annotate_models)

다음처럼 주석이 생성되서 컬럼 정보 찾으러 이 파일 저 파일 돌아다닐 필요가 없다.

```text
# == Schema Info
#
# Table name: line_items
#
#  id                  :integer(11)    not null, primary key
#  quantity            :integer(11)    not null
#  product_id          :integer(11)    not null
#  unit_price          :float
#  order_id            :integer(11)
#

 class LineItem < ActiveRecord::Base
   belongs_to :product
  . . .
```

## 설치

```bash
gem install annotate
```

또는 Bundler 사용 시, `Gemfile`에 추가 후 `bundle install`

```ruby
group :development do
  gem 'annotate'
end
```

레일즈 제너레이터를 사용해서 레일즈 프로젝트에 통합할 수 있다.

```bash
rails g annotate:install
```

`lib/tasks` 경로에 Rake 파일이 생성되는 데 여기 기본 값이 상세히 나와있으며 변경할 수 있다. 이 후 `rails db:*` 실행마다 설정해둔 옵션으로 자동 실행된다.

