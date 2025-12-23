# Deployment Guide
# Scientific Calculator - GitHub Pages

**Last Updated**: 2025-12-23  
**Deployment Method**: GitHub Actions → GitHub Pages

---

## 1. Prerequisites

### 1.1 Required
- GitHub 계정
- Git 설치
- Repository 생성 완료

### 1.2 Repository Structure
```
calculator/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions 워크플로우
├── index.html                  # 메인 HTML 파일
├── css/
│   └── styles.css              # 커스텀 CSS
├── js/
│   ├── main.js
│   ├── calculator.js
│   └── ...
└── README.md
```

---

## 2. GitHub Pages 설정

### 2.1 Repository Settings

1. **GitHub Repository 접속**
   - `https://github.com/<username>/<repository-name>`

2. **Settings → Pages 이동**
   - Repository 상단 메뉴에서 "Settings" 클릭
   - 좌측 사이드바에서 "Pages" 클릭

3. **Source 설정**
   - Build and deployment
   - Source: **"GitHub Actions"** 선택
   
   ![GitHub Pages Source](https://docs.github.com/assets/cb-47267/mw-1440/images/help/pages/publishing-source-drop-down.webp)

4. **Custom Domain (선택사항)**
   - Custom domain 입력 (예: `calculator.yourdomain.com`)
   - DNS 설정 필요

5. **HTTPS 강제 적용**
   - "Enforce HTTPS" 체크박스 활성화

---

## 3. GitHub Actions 워크플로우

### 3.1 워크플로우 파일 생성

`.github/workflows/deploy.yml` 파일이 이미 생성되어 있습니다.

### 3.2 워크플로우 구조

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]        # main 브랜치에 푸시 시 실행
  workflow_dispatch:          # 수동 실행 가능

jobs:
  build:                      # 빌드 및 검증
    - HTML 검증
    - JavaScript 문법 체크
    - 아티팩트 업로드
  
  deploy:                     # GitHub Pages 배포
    - 빌드 완료 후 실행
    - main 브랜치만 배포
```

### 3.3 워크플로우 트리거

**자동 배포**:
- `main` 브랜치에 코드 푸시 시 자동 실행
- Pull Request 생성 시 빌드 검증 (배포는 안 함)

**수동 배포**:
1. GitHub Repository → Actions 탭
2. "Deploy to GitHub Pages" 워크플로우 선택
3. "Run workflow" 버튼 클릭
4. 브랜치 선택 후 실행

---

## 4. 배포 프로세스

### 4.1 초기 배포

```bash
# 1. 로컬에서 코드 작성 및 테스트
# 2. Git 커밋
git add .
git commit -m "Initial commit: Scientific Calculator"

# 3. GitHub에 푸시
git push origin main

# 4. GitHub Actions 자동 실행
# - Actions 탭에서 진행 상황 확인
# - 약 1-2분 소요

# 5. 배포 완료 확인
# - https://<username>.github.io/<repository-name>/
```

### 4.2 업데이트 배포

```bash
# 1. 코드 수정
# 2. 커밋 및 푸시
git add .
git commit -m "feat: Add new feature"
git push origin main

# 3. 자동 재배포
# - GitHub Actions가 자동으로 실행
# - 배포 완료 후 변경사항 반영
```

---

## 5. 배포 확인

### 5.1 GitHub Actions 로그 확인

1. **Actions 탭 이동**
   - Repository → Actions

2. **워크플로우 실행 내역**
   - 최근 실행 목록 확인
   - 성공: ✅ 녹색 체크
   - 실패: ❌ 빨간 X

3. **상세 로그 확인**
   - 워크플로우 클릭
   - 각 단계별 로그 확인
   - 오류 발생 시 디버깅

### 5.2 배포 URL 확인

**기본 URL**:
```
https://<username>.github.io/<repository-name>/
```

**예시**:
- Username: `johndoe`
- Repository: `calculator`
- URL: `https://johndoe.github.io/calculator/`

### 5.3 배포 상태 확인

```bash
# GitHub CLI 사용 (선택사항)
gh workflow view "Deploy to GitHub Pages"
gh run list --workflow="Deploy to GitHub Pages"
```

---

## 6. 트러블슈팅

### 6.1 일반적인 문제

#### 문제 1: 404 Not Found
**원인**: GitHub Pages가 아직 활성화되지 않음
**해결**:
1. Settings → Pages에서 Source 확인
2. 워크플로우 재실행
3. 5-10분 대기 후 재확인

#### 문제 2: 워크플로우 실패
**원인**: 권한 문제
**해결**:
1. Settings → Actions → General
2. "Workflow permissions" 확인
3. "Read and write permissions" 선택
4. "Allow GitHub Actions to create and approve pull requests" 체크

#### 문제 3: CSS/JS 파일 로드 안 됨
**원인**: 상대 경로 문제
**해결**:
```html
<!-- 절대 경로 사용 -->
<link rel="stylesheet" href="/calculator/css/styles.css">
<script src="/calculator/js/main.js"></script>

<!-- 또는 상대 경로 -->
<link rel="stylesheet" href="./css/styles.css">
<script src="./js/main.js"></script>
```

### 6.2 디버깅 팁

```yaml
# deploy.yml에 디버그 단계 추가
- name: Debug - List files
  run: |
    echo "Current directory:"
    pwd
    echo "Files:"
    ls -la
    
- name: Debug - Check HTML
  run: |
    cat index.html
```

---

## 7. 성능 최적화

### 7.1 GitHub Pages 캐싱

GitHub Pages는 자동으로 CDN 캐싱을 제공합니다.

**Cache-Control 헤더** (자동 설정):
- HTML: `max-age=600` (10분)
- CSS/JS: `max-age=600`
- 이미지: `max-age=600`

### 7.2 배포 최적화

```yaml
# 불필요한 파일 제외
- name: Remove unnecessary files
  run: |
    rm -rf .git
    rm -rf .github
    rm -rf node_modules
    rm -rf tests
```

---

## 8. 모니터링

### 8.1 배포 알림 설정

**Slack 알림** (선택사항):
```yaml
- name: Notify Slack
  if: always()
  uses: 8398a7/action-slack@v3
  with:
    status: ${{ job.status }}
    webhook_url: ${{ secrets.SLACK_WEBHOOK }}
```

**이메일 알림**:
- GitHub Settings → Notifications
- "Actions" 알림 활성화

### 8.2 배포 히스토리

- **Deployments 탭**: Repository → Deployments
- 모든 배포 기록 확인
- 롤백 가능 (이전 커밋으로 되돌리기)

---

## 9. 보안 고려사항

### 9.1 Secrets 관리

민감한 정보는 GitHub Secrets 사용:

1. **Settings → Secrets and variables → Actions**
2. "New repository secret" 클릭
3. 이름 및 값 입력

```yaml
# 워크플로우에서 사용
- name: Use secret
  env:
    API_KEY: ${{ secrets.API_KEY }}
  run: echo "Secret loaded"
```

### 9.2 Branch Protection

**main 브랜치 보호**:
1. Settings → Branches
2. "Add branch protection rule"
3. 규칙 설정:
   - Require pull request reviews
   - Require status checks to pass

---

## 10. 고급 설정

### 10.1 Custom Domain 설정

**DNS 설정**:
```
# A 레코드
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153

# CNAME 레코드 (서브도메인)
calculator.yourdomain.com → <username>.github.io
```

**CNAME 파일 생성**:
```bash
echo "calculator.yourdomain.com" > CNAME
git add CNAME
git commit -m "Add custom domain"
git push
```

### 10.2 환경별 배포

```yaml
# Staging 환경
on:
  push:
    branches: [ develop ]

# Production 환경
on:
  push:
    branches: [ main ]
```

---

## 11. 체크리스트

### 11.1 배포 전 체크리스트

- [ ] 모든 파일이 커밋되었는가?
- [ ] 로컬에서 정상 작동하는가?
- [ ] HTML/CSS/JS 문법 오류가 없는가?
- [ ] 상대 경로가 올바른가?
- [ ] README.md가 작성되었는가?
- [ ] .gitignore가 설정되었는가?

### 11.2 배포 후 체크리스트

- [ ] GitHub Actions 워크플로우가 성공했는가?
- [ ] 배포 URL에서 정상 작동하는가?
- [ ] 모든 리소스(CSS/JS/이미지)가 로드되는가?
- [ ] 모바일에서 정상 작동하는가?
- [ ] 다크 모드가 작동하는가?
- [ ] 계산 기능이 정상 작동하는가?

---

## 12. 참고 자료

### 12.1 공식 문서
- [GitHub Pages 문서](https://docs.github.com/en/pages)
- [GitHub Actions 문서](https://docs.github.com/en/actions)
- [GitHub Actions - Pages 배포](https://github.com/actions/deploy-pages)

### 12.2 유용한 링크
- [GitHub Pages 상태](https://www.githubstatus.com/)
- [GitHub Community](https://github.community/)

---

## 13. 빠른 참조

### 13.1 주요 명령어

```bash
# 로컬 서버 실행
python -m http.server 8000

# Git 푸시 (배포 트리거)
git push origin main

# 워크플로우 상태 확인 (GitHub CLI)
gh run list

# 배포 URL 열기
open https://<username>.github.io/<repository-name>/
```

### 13.2 주요 URL

```
Repository: https://github.com/<username>/<repository-name>
Actions: https://github.com/<username>/<repository-name>/actions
Settings: https://github.com/<username>/<repository-name>/settings/pages
Deployed Site: https://<username>.github.io/<repository-name>/
```

---

**Document Version**: 1.0  
**Last Updated**: 2025-12-23  
**Author**: Antigravity AI
