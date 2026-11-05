# Jaehyeon's Portfolio

Hugo와 GitHub Pages로 만든 개인 포트폴리오 사이트입니다. 2026학년도 초급프로젝트 과제 1로 제작했습니다.

- 사이트: <https://jaehyeon3543.github.io/Portfolio_Practice/>
- 저장소: <https://github.com/Jaehyeon3543/Portfolio_Practice>
- 배포 기록(Actions): <https://github.com/Jaehyeon3543/Portfolio_Practice/actions>

## 사용 도구와 버전

| 도구 | 버전 | 용도 |
|---|---|---|
| Hugo (extended) | 0.167.0 | 사이트 빌드 (로컬·Actions 동일 버전) |
| Git | 2.53.0 | 버전 관리 |
| Python | 3.12 (Actions) | 배포용 빌드 스크립트 `.github/pages_build.py` 실행 |
| GitHub Actions / Pages | - | main에 push하면 자동 빌드·배포 |

로컬에서 사이트를 확인하는 데는 **Hugo extended 0.167.0만 있으면 됩니다.**
Actions 워크플로는 Python·Node.js·Go·Dart Sass도 설치하지만, 이 사이트의 로컬 빌드에는 필요하지 않습니다.

작성 환경: Ubuntu 26.04 (WSL2)

## 설치

1. Hugo **extended** 0.167.0을 설치합니다.
   [Hugo 릴리스 페이지](https://github.com/gohugoio/hugo/releases/tag/v0.167.0)에서 운영체제에 맞는 `hugo_extended_0.167.0_...` 파일을 받습니다.
   설치 후 버전을 확인합니다.
   ```bash
   hugo version
   # hugo v0.167.0-...+extended ...
   ```
2. 저장소를 내려받습니다.
   ```bash
   git clone https://github.com/Jaehyeon3543/Portfolio_Practice.git
   cd Portfolio_Practice
   ```

## 로컬에서 실행하기

> ⚠ Hugo 명령은 반드시 **`site/` 폴더 안에서** 실행합니다.
> 저장소 맨 위 폴더에서 실행하면 테마 원본 폴더를 사이트로 인식해 `/Portfolio_Practice/` 주소가 404가 됩니다.

```bash
cd site
hugo server
```

브라우저에서 <http://localhost:1313/Portfolio_Practice/> 를 엽니다.
사이트가 저장소 이름 하위 경로에 배포되므로 로컬에서도 `/Portfolio_Practice/`까지 붙여야 합니다.

배포용 결과물만 만들어 보려면:

```bash
cd site
hugo        # 결과물이 site/public/ 에 생성됨 (Git에는 올리지 않음)
```

## 폴더 구조

```text
Portfolio_Practice/
├─ site/                  ← 실제 사이트 (Hugo 명령은 여기서 실행)
│  ├─ hugo.json           사이트 설정
│  ├─ content/            글
│  ├─ layouts/            테마 템플릿을 덮어쓴 파일
│  ├─ assets/             CSS·JS (테마 파일을 덮어쓴 파일 포함)
│  ├─ i18n/               한국어 문구 (ko.toml)
│  ├─ static/             이미지
│  └─ themes/template/    Mana 테마 원본 (수정하지 않음)
├─ .github/workflows/     GitHub Pages 배포 워크플로
├─ LICENSE                Mana 테마 라이선스 (MIT)
└─ 그 밖의 파일·폴더        테마 ZIP 원본과 준비 스크립트 (사이트 빌드에는 쓰지 않음)
```

## 수정할 파일 위치

모든 사이트 파일은 `site/` 안에 있습니다. **테마 원본(`site/themes/template/`)은 수정하지 않고**, 바꿀 파일은 `site/layouts/`, `site/assets/`에 같은 경로로 복사해서 덮어씁니다.

| 바꾸고 싶은 것 | 파일 |
|---|---|
| 사이트 제목, 주소, 메뉴, GitHub·이메일 링크 | `site/hugo.json` |
| 홈 화면 전체 순서 (Hero → About → Projects → Experience → Blog) | `site/layouts/_default/home.html` |
| About (소개·사진·기술) | `site/layouts/partials/home/about.html` |
| Projects 카드 | `site/layouts/partials/home/projects.html` |
| Experience 타임라인 | `site/layouts/partials/home/experience.html` |
| 홈 섹션 디자인 | `site/assets/css/home.css` |
| Hero 디자인 | `site/assets/css/hero.css` |
| Footer (이메일·출처) | `site/layouts/partials/footer.html` |
| 버튼·메뉴 등의 한국어 문구 | `site/i18n/ko.toml` |
| 블로그 글 | `site/content/posts/` (프로젝트 글은 `site/content/posts/projects/`) |
| 이미지 | `site/static/` (주소는 `/Portfolio_Practice/파일명`) |

새 글은 `site/` 폴더에서 다음 명령으로 만듭니다. 만든 직후에는 `draft: true`라 사이트에 보이지 않으므로, 완성되면 `draft: false`로 바꿉니다.

```bash
hugo new content posts/글이름.md
```

## 수정 후 배포하고 확인하기

1. 수정한 내용을 커밋하고 main에 push합니다.
   ```bash
   git add <바꾼 파일>
   git commit -m "무엇을 바꿨는지 설명"
   git push
   ```
2. 저장소의 **Actions** 탭에서 `Deploy Hugo to GitHub Pages` 실행을 엽니다.
   `build`와 `deploy`가 모두 초록색 체크가 되면 배포가 끝난 것입니다.
3. <https://jaehyeon3543.github.io/Portfolio_Practice/> 를 열어 변경이 반영됐는지 확인합니다.
   반영이 안 보이면 강력 새로고침(Ctrl+Shift+R)을 합니다.

워크플로 설정은 `.github/workflows/hugo-pages.yml`에 있습니다. (수업 제공 스크립트 `prepare_github_pages.py`로 생성)

## 출처와 라이선스

### 외부 자료

| 자료 | 사용 위치 | 출처 | 라이선스 |
|---|---|---|---|
| Mana 테마 (Livour) | 사이트 전체 디자인·레이아웃 (`site/themes/template/`) | <https://github.com/Livour/hugo-mana-theme> | MIT (`LICENSE` 유지) |
| hugo-profile (gurusabarish) | About 기술 목록 스타일 (`site/assets/css/home.css`의 `.about-skills`) | <https://github.com/gurusabarish/hugo-profile> | MIT |
| Flaticon 아이콘 | 홈 Projects 카드 아이콘 (`site/static/free-icon-font-*.png`) | <https://www.flaticon.com/> | Flaticon 무료 라이선스 (출처 표기 조건, 사이트 footer에 표기) |

### AI로 생성한 자료

| 자료 | 사용 위치 | 생성 도구 |
|---|---|---|
| `claude_coffee.png` | Hero 이미지, 404 페이지, 파비콘 | Codex |

### 직접 제작한 자료

| 자료 | 사용 위치 |
|---|---|
| `me.jpg` | About 프로필 사진 (본인 사진) |
| `site/i18n/ko.toml` | 버튼·메뉴 한국어 문구 (테마의 `en.toml`을 참고해 직접 번역) |
| `site_screenshot.png` | 포트폴리오 글 화면 캡처 (직접 캡처) |
| `Pomodoro_site.png` | 포모도로 글 화면 캡처 (직접 캡처) |
| 소개·프로젝트 글, 홈 섹션 HTML 구조 | 직접 작성 |

### AI 도움을 받은 부분

AI(Claude)를 사용해 작성한 코드는 해당 위치에 **`(Claude 작성 → 학생 검토 후 적용)`** 주석을 남겼습니다. 주요 내용은 다음과 같습니다.

- Experience 타임라인 CSS (`site/assets/css/home.css`)
- 블로그 목록에 하위 폴더 글이 보이도록 한 수정 (`site/layouts/posts/list.html`)
- 홈 "프로젝트 더보기" → Projects 태그 필터 연결 (`site/assets/js/filters.js`)
- 홈·태그 링크가 `/Portfolio_Practice/` 하위 경로를 유지하도록 한 수정 (`site/layouts/` 의 breadcrumb, back-to-home, single, post-meta, post-tags-inline, taxonomy 파일)
- 글 상세 페이지 목차 제거 (`site/layouts/_default/single.html`)
- 프로젝트 카드 이미지·설명, 준비 중 카드 (`site/layouts/partials/home/projects.html`)
- 홈 Blog 섹션 "블로그 전체 보기" 버튼 스타일 (`home.css`의 `.blog-more`), footer의 Flaticon 출처 표기 (`site/layouts/partials/footer.html`)
- Hero 부제 대비 개선 (`site/assets/css/hero.css`), 좁은 화면 카드 잘림 수정 (`home.css`)
- 모바일 메뉴 키보드 초점 이동 (`site/assets/js/navigation.js`)
- 프로젝트 글 초안 (학생의 답변을 바탕으로 작성 후 학생이 수정)

AI가 제안한 내용은 모두 제가 확인한 뒤 적용했으며, 상세한 사용 사례와 검증 결과는 과제 보고서에 기록했습니다.
