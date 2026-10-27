---
name: issue-template
description: "Use when the user mentions @issue or asks to create a new OneDev issue. Provides the standard issue template format for creating well-structured issues."
user-invocable: true
---

When creating a new OneDev issue, use the following template:

## 📝 User Story

**As a** [user type / role]
**I want** [feature, fix, or change]
**So that** [business value or user benefit]

---

## 📖 Problem Description

**Current Behavior**
[What is happening right now?]

**Why This Is a Problem**
[Why this behavior is incorrect, confusing, risky, or inefficient.]

**Context**

* Platform: [Web / Mobile / Backend / Desktop / API]
* Environment: [Prod / Staging / Dev / Local]
* Affected area(s): [module, screen, service, API, workflow]

---

## 🔄 Steps to Reproduce

1. Open [application/system] as [user type].
2. Perform [action].
3. Navigate to [screen/page/tab].
4. Trigger [event: submit, cancel, delete, refresh, etc.].
5. Observe: [incorrect or unexpected behavior].

---

## 🎯 Expected Behavior

[Clearly describe what *should* happen instead.]

---

## ✅ Requirements

* [ ] Each entity/item/session has a **unique identifier**
* [ ] Removing/cancelling invalidates related identifiers or state
* [ ] No reuse of identifiers, references, or stale data
* [ ] Remaining entities continue functioning normally
* [ ] UI/state reflects the latest correct data
* [ ] System remains stable across retries and refreshes

---

## 🗒️ Implementation Checklist

* [ ] **Update core logic** → [business rules / workflow changes]
* [ ] **Validate data handling** → [IDs, tokens, cache, storage, cleanup]
* [ ] **Ensure UI/UX refresh** → [screen, component, state update]
* [ ] **Confirm UX flow** → [expected user journey and feedback]
* [ ] **Update documentation** → [README, API docs, comments]

---

## 🎯 Acceptance Criteria

* [ ] When [action] occurs, [expected result] happens
* [ ] Entity/state is correctly created, updated, or removed
* [ ] No incorrect redirection, reuse, or stale state appears
* [ ] System behaves consistently across refreshes and retries
* [ ] User experience is intuitive and predictable

---

## 📌 Additional Notes & Quality Checklist

### 🔧 Technical

* Backend/logic must update status correctly (`active`, `cancelled`, `deleted`, etc.)
* APIs/services must return **only valid and current entities**
* Handle race conditions, retries, and partial failures safely
* Ensure idempotency — repeated actions don't corrupt state
* Clean up unused resources (files, sessions, cache, references)

### 🎨 UX / UI

* UI must never show invalid or outdated state
* Provide clear user feedback (confirmation, error, loading)
* No silent failures — user should understand what happened
* Ensure behavior matches platform expectations (mobile vs web)

### 🧪 QA / Testing

* Test single and multiple entity scenarios
* Test edge cases:

  * Cancel → retry
  * Refresh during action
  * Offline / slow network
  * App background → resume
* Verify backward compatibility where applicable

### 📊 Monitoring & Logging

* Log key events and state transitions
* Track unexpected behavior or anomalies
* Ensure errors are observable and debuggable
