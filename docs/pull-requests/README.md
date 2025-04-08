# Pull Request Guidelines

## Creating Pull Requests

### PR Status and Ownership
* Every PR that is not ready for review must be marked as **Draft**
* Each PR must have at least two assigned reviewers
* If you have a colleague who works on the same module or same task - their review is **required**
* The PR creator is fully responsible for their PR through the entire lifecycle
* **PR creator is responsible** for resolving merge conflicts

### PR Content Requirements
* Include screenshot(s) of the UI implementation to help reviewers understand the changes

### Approval Requirements
* **At least 2 approvals are required** before merging any PR
* One of these approvals must be from a colleague working on the same module/task when applicable

### 🌿 Branching Strategy

Each branch must include the project ticket number for traceability:

1. **`main`** – Stable production branch.
2. **`develop`** – Integration branch for all features.
3. **`feature/PROJECT-XXX-description`** – New features (e.g., `feature/PROJECT-001-user-authentication`).
4. **`bugfix/PROJECT-XXX-description`** – Bug fixes (e.g., `bugfix/PROJECT-045-fix-login-error`).
5. **`hotfix/PROJECT-XXX-description`** – Critical fixes for `main`.
6. **`release/{version}`** – Prepares a release before merging into `main`.
7. **`chore/PROJECT-XXX-description`** – Routine tasks (e.g., `chore/PROJECT-010-update-dependencies`).

### 📜 Commit Message Format

Format:

```
<type>: <message>
```

Example:

```
feat: add Google login
```

Commit Types:

- **`feat`** – A new feature
- **`fix`** – A bug fix
- **`docs`** – Documentation updates
- **`style`** – Code style changes (no logic changes)
- **`refactor`** – Code restructuring (no functional changes)
- **`perf`** – Performance improvements
- **`test`** – Adding or updating tests
- **`chore`** – Maintenance tasks (e.g., CI/CD, dependencies)

### PR Creator Checklist
- [ ] Meets all [Definition of Done](/definition-of-done/) criteria
- [ ] UI screenshots are included
- [ ] Branch follows naming convention
- [ ] Commits follow message format

### Merging Guidelines
* Only merge after receiving **at least 2 approvals**
* One approval must be from a colleague working on the same module/task when applicable
* Squash commits when appropriate for a cleaner history
* Delete the branch after merging
* Verify the build succeeds after merging

---

## Reviewing Pull Requests

### Review Timeline
* Initial review should happen within 24 hours of PR submission
* Prioritize reviews for critical fixes and blockers

### Review Thoroughness
* Verify that the code meets all requirements in the [Definition of Done](/definition-of-done/), which can be confirmed through code review
* **Code Quality**: Check for maintainability, readability, and adherence to project conventions? (TBD)
* **Functionality**: Ensure the code fulfills its intended purpose? (TBD)
* **Performance**: Watch for inefficient code or potential bottlenecks? (TBD)
* **Security**: Identify any security vulnerabilities or risks? (TBD)

### Review Comments
* Be specific about what needs to be changed and why
* Offer suggestions for improvement when possible
* Use "Request changes" for required modifications
* Use "Approve" only when confident the code is ready to merge

### Reviewer Checklist
- [ ] Code follows project standards
- [ ] UI matches design (for frontend changes)
- [ ] No unused code or commented-out code
- [ ] Error handling is appropriate
- [ ] Edge cases are considered
- [ ] No security vulnerabilities
- [ ] Documentation is updated if necessary