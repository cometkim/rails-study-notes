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

## 사용법

```bash
rubocop # bundle exec rubocop
```

실행하면 기본 출력 포맷으로 분석결과를 보여준다.

또한 `--auto-correct` 옵션을 통한 자동 코드 포매팅도 지원하니 pre-commit hook 등과 연계해도 좋다.

## 레일즈 설정

레일즈는 공식 [RuboCop 설정](https://github.com/rails/rails/blob/master/.rubocop.yml)을 가지고 있다.

```text
inherit_gem:
  - https://raw.githubusercontent.com/rails/rails/master/.rubocop.yml
```

위와 같이 레일즈의 `.rubocop.yml` 설정을 상속해서 사용한다.

레일즈의 공식 RuboCop은 Ruby 2.4 버전을 타겟으로 하는 데 각자 프로젝트에 맞는 루비 버전으로 변경한다.

```diff
+AllCops:
+  TargetRubyVersion: 2.5
```

## 설정 파일 리소스

위의 레일즈 공식 설정파일 외에도, 빅브라더들이 오픈소스로 공개한 스타일 가이드가 있으니 팔로우 하거나 확장해서 사용하면 좋다.

* [Ruby 커뮤니티 코드 스타일 가이드](https://github.com/rubocop-hq/ruby-style-guide) \(RuboCop 기본 설정으로 지원\)
* [Rails 코드 스타일 가이드](https://github.com/rails/rails/blob/master/.rubocop.yml) \(커뮤니티 표준 가이드의 많은 부분을 무시하도록 되어있다\)
* [GitHub 코드 스타일 가이드](https://github.com/github/rubocop-github)
* [AirBnB 코드 스타일 가이드](https://github.com/airbnb/ruby)

