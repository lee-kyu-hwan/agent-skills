## 배경                                              
                                                       
  현재 프로젝트 내 `.claude/skills/`에 PR 리뷰 스킬이  
  존재합니다:                                          
  - `review-pr-mobile` - React Native/Expo 모바일 PR   
  리뷰                                                 
  - `review-pr-web` - React/Next.js 웹 PR 리뷰         
                                                       
  이 스킬들을 여러 AI 에이전트(Claude, Codex, Gemini   
  등)에서 재사용할 수 있도록 별도 레포지토리로         
  분리하고자 합니다.                                   
                                                       
  ## 참고 레포지토리                                   
                                                       
  - [vercel-labs/agent-skills](https://github.com/verce
  l-labs/agent-skills)                                 
  - [anthropics/skills](https://github.com/anthropics/s
  kills)                                               
  - [Agent Skills 표준](https://agentskills.io)        
                                                       
  ## 목표                                              
                                                       
  1. **별도 GitHub 레포지토리 생성** (`agent-skills`   
  또는 `pr-review-skills`)                             
  2. **Agent Skills 표준 구조 적용**                   
  3. **여러 AI 도구에서 설치/사용 가능하도록 구성**    
                                                       
  ## 제안 레포지토리 구조                              
                                                       
  agent-skills/                                        
  ├── skills/                                          
  │   ├── review-pr-mobile/                            
  │   │   └── SKILL.md                                 
  │   └── review-pr-web/                               
  │       └── SKILL.md                                 
  ├── AGENTS.md              # Codex/Copilot용         
  ├── CLAUDE.md              # Claude Code용           
  ├── .gemini/                                         
  │   └── instructions.md    # Gemini용                
  └── README.md                                        
                                                       
  ## 설치 방법 (구현 후)                               
                                                       
  ```bash                                              
  # Claude Code                                        
  /install-github-skill your-org/agent-skills          
                                                       
  # npx (add-skill CLI)                                
  npx add-skill your-org/agent-skills                  
                                                       
  작업 항목                                            
                                                       
  - 새 레포지토리 생성                                 
  - Agent Skills 표준에 맞게 폴더 구조 정리            
  - AGENTS.md, CLAUDE.md, .gemini/instructions.md 작성 
  - README.md 작성 (설치 방법, 스킬 목록, 사용 예시)   
  - 기존 프로젝트에서 새 레포 스킬 참조하도록 변경     
                                                       
  레포지토리 이름 후보                                 
  ┌──────────────────┬──────────────────────────┐      
  │       이름       │           용도           │      
  ├──────────────────┼──────────────────────────┤      
  │ agent-skills     │ 다양한 스킬 추가 예정 시 │      
  ├──────────────────┼──────────────────────────┤      
  │ pr-review-skills │ PR 리뷰 스킬에 특화      │      
  ├──────────────────┼──────────────────────────┤      
  │ ```              │                          │      
  └──────────────────┴──────────────────────────┘  
