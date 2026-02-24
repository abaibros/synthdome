# 🌐 SynthDome 웹사이트 - GitHub Pages + 커스텀 도메인 설정 가이드

## 📋 목차
1. [GitHub Pages 활성화](#1-github-pages-활성화)
2. [커스텀 도메인 연결](#2-커스텀-도메인-연결-synthdomecom)
3. [DNS 설정](#3-dns-설정)
4. [HTTPS 설정](#4-https-설정)
5. [확인 및 테스트](#5-확인-및-테스트)

---

## 1️⃣ GitHub Pages 활성화

### 단계별 설정:

1. **GitHub 저장소로 이동**
   ```
   https://github.com/abaibros/synthdome
   ```

2. **Settings 탭 클릭**
   - 저장소 상단의 "Settings" 클릭

3. **Pages 메뉴로 이동**
   - 왼쪽 사이드바에서 "Pages" 클릭

4. **Source 설정**
   - **Branch**: `main` 선택
   - **Folder**: `/ (root)` 선택
   - **Save** 버튼 클릭

5. **배포 대기**
   - GitHub Actions가 자동으로 실행됩니다
   - 약 1-3분 정도 소요됩니다
   - "Your site is live at https://abaibros.github.io/synthdome/" 메시지 확인

---

## 2️⃣ 커스텀 도메인 연결 (synthdome.com)

### GitHub Pages 설정:

1. **Settings > Pages로 이동**

2. **Custom domain 섹션**
   - "Custom domain" 입력란에 `synthdome.com` 입력
   - **Save** 버튼 클릭

3. **DNS 체크 대기**
   - "DNS check in progress..." 메시지 표시
   - DNS 설정이 완료되면 체크마크로 변경됩니다

4. **HTTPS 적용**
   - "Enforce HTTPS" 체크박스 활성화 (DNS 확인 후 가능)
   - 자동으로 Let's Encrypt SSL 인증서 발급

---

## 3️⃣ DNS 설정

### synthdome.com 도메인의 DNS 레코드 설정:

#### A 레코드 (Apex 도메인용):

도메인 등록 업체(예: GoDaddy, Namecheap, Cloudflare 등)의 DNS 관리 페이지에서 다음 A 레코드를 추가하세요:

```
Type: A
Name: @ (또는 비워두기)
Value/Points to: 
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
TTL: 3600 (또는 1 hour)
```

**⚠️ 중요**: 4개의 A 레코드를 모두 추가해야 합니다!

#### CNAME 레코드 (www 서브도메인용):

```
Type: CNAME
Name: www
Value/Points to: abaibros.github.io
TTL: 3600 (또는 1 hour)
```

### DNS 설정 예시 (각 도메인 제공업체별):

#### Cloudflare:
1. Dashboard → DNS → Records
2. Add record
3. Type: A, Name: @, IPv4 address: (위 4개 IP 각각 추가)
4. Add record
5. Type: CNAME, Name: www, Target: abaibros.github.io

#### GoDaddy:
1. My Products → Domains → DNS
2. Add → A Record
3. Name: @, Value: (위 4개 IP 각각 추가)
4. Add → CNAME Record
5. Name: www, Value: abaibros.github.io

#### Namecheap:
1. Domain List → Manage → Advanced DNS
2. Add New Record
3. Type: A Record, Host: @, Value: (위 4개 IP 각각 추가)
4. Add New Record
5. Type: CNAME, Host: www, Target: abaibros.github.io

---

## 4️⃣ HTTPS 설정

### 자동 SSL 인증서 발급:

1. **DNS 전파 대기**
   - DNS 설정 후 전 세계에 전파되기까지 **최대 24-48시간** 소요
   - 일반적으로 1-2시간 내에 완료

2. **GitHub Pages에서 HTTPS 활성화**
   - Settings > Pages로 이동
   - "Enforce HTTPS" 체크박스 활성화
   - GitHub가 자동으로 Let's Encrypt SSL 인증서 발급

3. **확인**
   - `https://synthdome.com`으로 접속 시 자물쇠 아이콘 확인

---

## 5️⃣ 확인 및 테스트

### DNS 전파 확인:

#### 온라인 도구 사용:
```
https://www.whatsmydns.net/
```
- synthdome.com 입력
- A 레코드 선택
- 전 세계 DNS 서버에서 확인

#### 명령어로 확인 (터미널):
```bash
# A 레코드 확인
dig synthdome.com +short

# CNAME 레코드 확인
dig www.synthdome.com +short

# Windows에서
nslookup synthdome.com
```

### 웹사이트 접속 테스트:

1. **Apex 도메인**
   ```
   http://synthdome.com
   https://synthdome.com (HTTPS 설정 후)
   ```

2. **WWW 서브도메인**
   ```
   http://www.synthdome.com
   https://www.synthdome.com (HTTPS 설정 후)
   ```

3. **GitHub Pages URL (백업)**
   ```
   https://abaibros.github.io/synthdome/
   ```

---

## 📊 타임라인 요약

| 단계 | 예상 시간 |
|------|----------|
| GitHub Pages 활성화 | 1-3분 |
| DNS 레코드 추가 | 5분 |
| DNS 전파 | 1-48시간 (보통 1-2시간) |
| HTTPS 인증서 발급 | 5-10분 (DNS 전파 후) |
| **총 소요 시간** | **1-48시간** |

---

## 🔧 문제 해결

### 1. "DNS check failed" 오류
- **원인**: DNS 레코드가 아직 전파되지 않음
- **해결**: 1-2시간 후 다시 시도

### 2. "CNAME already taken" 오류
- **원인**: 다른 GitHub 저장소가 같은 도메인 사용 중
- **해결**: 기존 CNAME 설정 제거 후 재설정

### 3. 404 오류 발생
- **원인**: 배포가 완료되지 않음
- **해결**: 
  - Actions 탭에서 배포 상태 확인
  - main 브랜치에 index.html 파일 존재 확인

### 4. 동영상이 재생되지 않음
- **원인**: 파일 크기가 큼 (46MB)
- **해결**:
  - 브라우저 캐시 삭제
  - 고속 인터넷 연결 확인
  - Chrome/Safari 최신 버전 사용

### 5. CSS/JS 파일 404 오류
- **원인**: 파일 경로 문제
- **해결**: 
  - 브라우저 개발자 도구(F12) → Console 확인
  - 파일 경로가 상대 경로인지 확인

---

## 📞 현재 설정 상태

### ✅ 완료된 작업:
- ✅ CNAME 파일 생성 (synthdome.com)
- ✅ main 브랜치에 전체 웹사이트 머지 완료
- ✅ 동영상 배경 포함 (assets/synthdome-hero.mp4)
- ✅ 프리미엄 디자인 완료
- ✅ 반응형 레이아웃 완료
- ✅ GitHub 저장소에 푸시 완료

### 🔄 진행 필요:
1. **GitHub Pages 활성화** (위 1단계)
2. **DNS 레코드 설정** (위 3단계)
3. **HTTPS 활성화** (DNS 전파 후)

---

## 🌐 접속 URL (설정 완료 후)

### 최종 프로덕션 URL:
```
https://synthdome.com
https://www.synthdome.com
```

### 백업 URL (현재 사용 가능):
```
https://abaibros.github.io/synthdome/
```

---

## 📚 추가 리소스

- [GitHub Pages 공식 문서](https://docs.github.com/en/pages)
- [커스텀 도메인 설정 가이드](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [DNS 설정 가이드](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

---

## 📞 연락처

문의사항이 있으시면 아래로 연락주세요:

- **전화**: +82)10-8496-1440 / +82)10-4224-2020
- **이메일**: synthdome.ceo@gmail.com
- **주소**: 서울시 성동구 성수1동 태성빌딩

---

**✅ 작성일**: 2026-02-24  
**✅ 저장소**: https://github.com/abaibros/synthdome  
**✅ 상태**: 설정 준비 완료

---

**🎉 이제 위 가이드를 따라하시면 synthdome.com으로 웹사이트에 접속하실 수 있습니다!**
