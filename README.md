# CareTrack WA

A bright, hopeful web platform for Washington caregivers/parents supporting special-needs dependents through **guardianship and conservatorship** processes.

## Vision

CareTrack WA helps families understand what to do next, when to do it, and where county-level differences may affect required steps.

## Core Product Goals

- Require secure login so each family can manage private case details.
- Build a guided experience that learns enough about each situation to offer relevant process steps.
- Support Washington-wide flows with county-specific variations where they exist.
- Send proactive reminder emails at 120, 90, 60, and 30 days before deadlines.
- Use a bright, cheerful, and hopeful visual design language to reduce stress.

## Primary User Journey

1. **Create account / login**
   - Email + password or passwordless magic links.
   - Optional MFA for sensitive legal records.
2. **Answer guided intake**
   - County, dependent age, current legal status, urgency, and existing court history.
3. **Receive personalized roadmap**
   - Clear checklist of filing milestones, document prep, hearings, and follow-up actions.
4. **Track progress**
   - Mark steps complete, upload notes/documents, and share read-only progress with trusted helpers.
5. **Stay ahead of deadlines**
   - Automatic reminder cadence (120/90/60/30 days).

## Suggested Feature Set (MVP)

### 1) Authentication & Privacy
- Account registration and login.
- Encrypted personal and case metadata at rest.
- Role model:
  - Primary caregiver (owner)
  - Collaborator (trusted family member/advocate)
  - Read-only viewer

### 2) Adaptive Intake + Eligibility Logic
- Dynamic questionnaire that branches based on user answers.
- Data collected only as needed to determine relevant process path.
- Intake outputs:
  - Recommended track: guardianship and/or conservatorship
  - County-specific considerations
  - Priority tasks and estimated timeline

### 3) Washington Process Knowledge Base
- Canonical statewide baseline steps.
- County overlays (King, Pierce, Snohomish, etc.) for local form, filing, or scheduling differences.
- Versioned content model so legal/process updates can be audited and rolled out safely.

### 4) Roadmap + Task Management
- Milestone timeline with due dates and dependencies.
- Tasks include tips, plain-language explanations, and links to official court resources.
- Status model: Not Started / In Progress / Waiting / Completed.

### 5) Reminder & Notification Engine
- Email triggers at **120/90/60/30 days** before due date.
- Digest mode for families managing multiple dependents.
- Delivery tracking (queued/sent/bounced) and retry policy.

### 6) Sharing & Collaboration
- Invite collaborators by email.
- Granular sharing permissions by dependent/case.
- Activity log for transparency.

### 7) Tone & Accessibility
- Friendly, uplifting copy and color system.
- WCAG AA-compliant contrast and keyboard accessibility.
- Multi-language-ready copy model (starting with English).

## Proposed Technical Architecture

### Frontend
- **Next.js + TypeScript** for server-rendered app and dashboard UX.
- Component system emphasizing hopeful visuals (warm gradients, supportive microcopy, celebratory progress states).

### Backend
- **PostgreSQL** for users, dependents, tasks, county-rule versions, and audit logs.
- **API layer** (Next.js Route Handlers or separate service) for workflow orchestration.
- **Background job queue** for scheduled reminders and digest emails.

### Notifications
- Email provider integration (e.g., SendGrid/Postmark).
- Scheduled jobs created per due date with offsets of 120/90/60/30 days.
- Idempotency keys to prevent duplicate sends.

### Security
- Strong password hashing, secure session management, CSRF protection.
- Encryption for sensitive case metadata.
- Immutable audit logs for critical user and content changes.

## Example Domain Model

- `User`
- `Household`
- `Dependent`
- `Case`
- `CountyRuleSet`
- `Milestone`
- `Task`
- `ReminderSchedule`
- `NotificationEvent`
- `Invite`

## County Variation Strategy

1. Start from statewide baseline process template.
2. Apply county override rules (forms, hearing lead times, local clerk expectations).
3. Display “why this differs” notes to keep families informed and confident.
4. Track source references and effective dates per county rule entry.

## 30/60/90-Day Build Plan

### Days 1–30
- Product discovery interviews with WA caregivers and legal advocates.
- Draft process maps and county-variation schema.
- Build auth, intake v1, and basic task timeline.

### Days 31–60
- Add county overlays for highest-population counties.
- Implement reminder scheduler and notification templates.
- Launch private alpha with 10–20 families.

### Days 61–90
- Expand county coverage and quality checks.
- Add collaborator permissions and progress sharing.
- Improve onboarding tone/design based on caregiver feedback.

## Compliance & Legal Positioning

- Position platform as legal process guidance and organization support, not legal advice.
- Keep clear disclaimers and links to official Washington court resources.
- Establish a legal content review cadence and change-approval workflow.

## Next Steps

1. Confirm target counties for initial launch.
2. Validate intake questions with legal/advocacy stakeholders.
3. Build clickable prototype for caregiver usability testing.
4. Implement MVP with reminder pipeline and county-rule engine.
