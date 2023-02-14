---
layout: single
title: Project Github
categories: Team_Project
tags: [project]
---

<br/>

# 프로젝트 Github

## 📁 Github Repository

### 👉 Github Repository에 꼭 필요한 파일

<hr/>

#### ▶️ README.md

github 오픈 소스에 들어가면, 가장 먼저 확인 할 수 있는 정보가 README.md 파일에 담긴 정보이다.
README.md 파일을 적는 양식은 따로 존재하지 않지만, 대체로 어떻게 하면 해당 오픈소스를 활용할 수 있는지에 대한 상세한 정보가 작성되어 있다.<br/>

##### Pre-Project README.md에 꼭 포함해야 할 내용

- 프로젝트 이름
- 프로젝트 핵심 기능 소개
- 팀원 소개

#### ▶️ .gitignore

.gitignore 파일은 git으로 관리하지 않는 파일 모음이다. 여기에는 개인이 따로 관리해야 하는 중요한 secret token이나, 다른 동료와 공유할 필요가 없는 설정 파일, 그 외 공유할 필요 없는 파일을 기록하면 git이 이를 파악하지 않고, push 할 때도 리포지포리에 push 되지 않는다.

#### ▶️ LICENSE

해당 코드의 라이센스를 표기한다. 깃허브에 public하게 공개된 리포지토리도 라이센스에 따라서 사용을 할 수도 있고, 하지 못 할 수도 있으니 사용할 떄 라이센스를 잘보고 사용해야 한다. 회사에서 사용하는 코드는 private으로 관리하고, 외부에 공개하지 않아 따로 라이센스 정보를 표기하지 않기도 한다. 하지만 회사에서 작성하는 코드가 public으로 공개될 경우, LICENSE를 명확하게 표기해야 한다.

### 👉 Project 관리에 활용할 수 있는 Github 기능

<hr/>

#### ▶️ Issue

Issue는 말 그대로 프로젝트에 새로운 기능을 제안하거나, 버그를 찾아 제보하는 등 프로젝트의 이슈를 의미한다.<br/>

##### Pre-Project에서의 사용

Pre-Project에서는 Issue를 하나의 칸반 티켓처럼 사용한다.

#### ▶️ Milestone

Milestone은 이정표 역할을 하며, 태스크 카드(Issue)를 그룹화하는 데 사용한다. Milestone에 연결된 태스크 카드(Issue)가 종료되면 Milestone마다 진행 상황이 업데이트되는 것을 볼 수 있다. 이 Milestone 기능을 통해 연관된 이슈의 추적과 진행 상황을 한눈에 파악할 수 있는 장점이 있다.

##### Pre-Project에서의 사용

Pre-Project에서는 Bare Minimum, Advanced Challange, Nightmare를 표시하기 위해 사용한다.

#### ▶️ Pull Request

Pull Request는 내가 작업한 내용을 중요 git branch에 합칠 수 있는지 확인하는 요청이다. Github에서는 Pull Request를 Pull Request에 커밋한 코드를 따로 선택하여 해당 부분에 코멘트를 달 수 있다. 현장에서도 Pull Request를 보면서 코멘트를 남기며 코드 리뷰를 진행하기 때문에 Pull Request 과정에 익숙해 지는 것이 중요하다.

#### ▶️ Project

Project는 Github 내에서 업무 관리를 해줄 수 있게 돕는 새로운 기능이다.

##### Pre-Project에서의 사용

Pre-Project에서는 이 Project 기능을 이용하여 칸반 보드를 생성하고, 칸반으로 Pre-Project의 업무 흐름을 관리한다.
