# RuboCop

[RuboCop](https://github.com/rubocop-hq/rubocop)은 루비 코드 정적 분석기이다.

프로젝트마다 이러한 도구의 룰\(Cop이라 부름\)셋을 잘 설정해두면 코드 스타일 가이드로써 큰 역할을 한다.

코드 스타일을 명시적으로 제한해서 일관성을 향상 시키는 건 물론, 자동화가 가능하니 CI 통합을 통해 코드 리뷰에 들어가는 비용을 큰 폭으로 줄일 수 있기에 선택 아닌 필수인 도구 중 하나 이다.

* 문서: [http://docs.rubocop.org/en/latest/](http://docs.rubocop.org/en/latest/) ~~문서 구려~~

## 설치

`gem install rubocop`

번들러 사용 시 `Gemfile`에 추가 후 `bundle install` 

```ruby
gem 'rubocop', require: false
```

## 설정 파일

프로젝트 루트에 `.rubocop.yml` 파일을 추가해서 설정을 변경할 수 있다.

레일즈 설정은 기본으로 내장된 Cop 중에 [레일즈 전용 카테고리](https://docs.rubocop.org/en/latest/cops/#rails)가 있으니 이걸 사용하면 된다.

기본 설정에서는 Ruby 2.4 버전을 타겟으로 하는 데 각자 프로젝트에 맞는 루비 버전으로 변경해주면 좋다.

```diff
+AllCops:
+  TargetRubyVersion: 2.5
+  Exclude:
+    - 'db/schema.rb'
+    - 'node_modules/**/*'
+
+Rails:
+  Enabled: true
```

## 사용법

```bash
rubocop # bundle exec rubocop
```

실행하면 기본 출력 포맷으로 분석결과를 보여준다.

또한 `--auto-correct` 옵션을 통한 자동 코드 포매팅도 지원하니 pre-commit hook 등과 연계해도 좋다.

```bash
rails g rubocop:install
```

위처럼 레일즈 제너레이터를 사용해서 Rake 태스크로 통합할 수도 있다.

```text
$ rake -T

rake rubocop                            # Run RuboCop
rake rubocop:auto_correct               # Auto-correct RuboCop offenses
```

## 설정 파일 리소스

위의 레일즈 공식 설정파일 외에도, 빅브라더들이 오픈소스로 공개한 스타일 가이드가 있으니 팔로우 하거나 확장해서 사용하면 좋다.

* [Ruby 커뮤니티 코드 스타일 가이드](https://github.com/rubocop-hq/ruby-style-guide) \(RuboCop 기본 설정\)
* [Rails 코드 스타일 가이드](https://github.com/rails/rails/blob/master/.rubocop.yml)
* [GitHub 코드 스타일 가이드](https://github.com/github/rubocop-github)
* [AirBnB 코드 스타일 가이드](https://github.com/airbnb/ruby)



