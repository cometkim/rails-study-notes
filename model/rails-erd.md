# Rails ERD

## 소개

ActiveRecord 모델들과 Associations로 부터 다이어그램을 뽑아주는 잼이다.

* [Gem](https://rubygems.org/gems/rails-erd)
* [Source](https://github.com/voormedia/rails-erd)
* [Diagram Gallery](https://voormedia.github.io/rails-erd/gallery.html)

ERD라고는 하지만, 막상 보면 액티브레코드 시각화에 가깝다.

ERD 산출물로써는 활용하지 못하더라도 모델링이 잘못됐다면 이쁜 그림이 나올 수가 없으니 피드백으로써 꽤 쓸만하다.

## 설치

시각화 하는데 [Graphviz](https://www.graphviz.org)를 사용한다. 개발 환경에 graphviz가 설치되어 있지 않다면 설치해야한다.

`Gemfile`의 `:development` 그룹에 잼 선언을 추가한 후, `bundle install`을 실행한다.

```ruby
group :development do
  gem 'rails-erd'
end
```

제공되는 레일즈 제너레이터를 사용해 레일즈와 통합할 수 있다.

```bash
rails g erd:install
```

## 설정

프로젝트 루트 경로에 `.erdconfig` 파일을 생성해서 기본 설정을 변경할 수 있다.

```yaml
attributes:
  - content
  - foreign_key
  - inheritance
disconnected: true
filename: erd
filetype: pdf
indirect: true
inheritance: false
markup: true
notation: simple
orientation: horizontal
polymorphism: false
sort: true
warn: true
title: sample title
exclude: null
only: null
only_recursion_depth: null
prepend_primary: false
cluster: false
splines: spline
```

