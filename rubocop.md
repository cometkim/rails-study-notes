# RuboCop 사용

[RuboCop](https://github.com/rubocop-hq/rubocop)은 루비 코드 정적 분석기이다.

* 문서: [http://docs.rubocop.org/en/latest/](http://docs.rubocop.org/en/latest/) ~~문서 구려~~

## 설치

`gem install rubocop`

번들러 사용 시 `Gemfile`에 추가 후 `bundle install` 

```ruby
gem 'rubocop', require: false
```

## 설정 파일

프로젝트 루트에 `.rubocop.yml` 파일을 추가해서 설정을 변경할 수 있다.

## 레일즈와 사용하기

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

## 사용하기

```bash
rubocop # bundle exec rubocop
```

실행하면 기본 출력 포맷으로 분석결과를 보여준다.

또한 `--auto-correct` 옵션을 통한 자동 코드 포매팅도 지원하니 pre-commit hook 등과 연계해도 좋다.

