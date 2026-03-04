# Code Analysis Report: index.html

**Analysis Date**: March 2, 2026  
**File**: index.html  
**Total Lines**: 4175

---

## 1. UNUSED FIREBASE MODULES ✗

### 1.1 Firestore Module (firebase-firestore-compat)
- **Status**: ❌ UNUSED
- **Lines**: 1847
- **Declaration**: `<script src="https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore-compat.js"></script>`
- **Global**: `const db = firebase.firestore();` (Line 1851)
- **Reason**: The variable `db` is declared but never referenced in the code. All data is stored using `localStorage` instead.
- **Impact**: Unused library loads unnecessarily
- **Recommendation**: ✂️ REMOVE

### 1.2 Storage Module (firebase-storage-compat)
- **Status**: ❌ UNUSED
- **Lines**: 1848
- **Declaration**: `<script src="https://www.gstatic.com/firebasejs/10.7.0/firebase-storage-compat.js"></script>`
- **Global**: `const storage = firebase.storage();` (Line 1852)
- **Reason**: The variable `storage` is declared but never used. Photos are stored as base64 data URLs in localStorage.
- **Impact**: Unused library loads unnecessarily
- **Recommendation**: ✂️ REMOVE

### 1.3 Analytics Module (firebase-analytics-compat)
- **Status**: ❌ UNUSED
- **Lines**: 1845
- **Declaration**: `<script src="https://www.gstatic.com/firebasejs/10.7.0/firebase-analytics-compat.js"></script>`
- **Global**: `const analytics = firebase.analytics();` (Line 1850)
- **Reason**: Initialized but never called anywhere in the code. No tracking or analytics functionality is used.
- **Impact**: Unused library loads unnecessarily
- **Recommendation**: ✂️ REMOVE

---

## 2. UNUSED GLOBAL VARIABLES 🔴

### 2.1 `streamActive` Variable
- **Declaration**: Line 1868
- **Status**: ❌ UNUSED
- **Code**: `let streamActive = false;`
- **Reason**: Never read or written after initialization. Actual stream state is tracked with `visitorStreamActive` and `ceremonyStreamActive`.
- **Recommendation**: ✂️ REMOVE

### 2.2 `createTabUnlocked` Variable
- **Declaration**: Line 1921
- **Status**: ❌ UNUSED
- **Code**: `let createTabUnlocked = true;`
- **Reason**: This variable is set but never checked. The comment "protection by password has been removed, always unlocked" indicates old code.
- **Related**: Also unused: `ceremonyTabUnlocked` (Line 1922)
- **Recommendation**: ✂️ REMOVE (Lines 1921-1922)

### 2.3 `ceremonyTabUnlocked` Variable
- **Declaration**: Line 1922
- **Status**: ❌ UNUSED
- **Code**: `let ceremonyTabUnlocked = true;`
- **Reason**: Same as above - never checked in the code
- **Recommendation**: ✂️ REMOVE

---

## 3. UNUSED FUNCTIONS 🔵

### 3.1 ALL Firestore Helper Functions (DEAD CODE BLOCK)
**Status**: ❌ COMPLETELY UNUSED  
**Lines**: 1759-1824  
**Reason**: These functions were intended for Firestore integration but all data operations use `localStorage` instead.

Functions to remove:
- `ajouterUneNote()` (Lines 1759-1774) - Creates a note but never called
- `ajouterDocument()` (Lines 1776-1788) - Generic document creation but never called
- `obtenirDocuments()` (Lines 1790-1806) - Retrieve documents but never called
- `ecouterDocuments()` (Lines 1808-1821) - Real-time listener but never called
- `obtenirDocumentsFiltrés()` (Lines 1823-1840) - Query with filters but never called
- `mettreAJourDocument()` (Lines 1842-1851) - Update function but never called
- `supprimerDocument()` (Lines 1853-1861) - Delete function but never called

**Recommendation**: ✂️ REMOVE ALL (Lines 1759-1824)

### 3.2 Firebase Authentication Functions (UNUSED)
**Status**: ❌ MOSTLY UNUSED  
**Lines**: 1688-1755

Functions to remove:
- `entrerAvecGoogle()` (Lines 1703-1719) - Never called anywhere
- `sinscrireAvecEmail()` (Lines 1726-1737) - Only called from `handleSignUp()` which is never triggered
- `entrerAvecEmail()` (Lines 1741-1753) - Never called anywhere
- `sortirDeLaCabane()` (Lines 1757-1768) - Never called anywhere

**Recommendation**: ✂️ REMOVE (Lines 1703-1768) OR keep only if UI elements are added later

### 3.3 `openAboutModal()` and `closeAboutModal()` - QUESTIONABLE
- **Lines**: 1863-1868
- **Status**: ⚠️ USED (called from nav-tab in HTML via onclick)
- **Decision**: KEEP (legitimately used)

### 3.4 `openSignUpModal()` and `closeSignUpModal()`
- **Lines**: 1870-1876
- **Status**: ❌ UNUSED
- **Reason**: Functions exist but `signupModal` element is set to `display:none` by default (line 1626) and there's no button to open it
- **Recommendation**: ✂️ REMOVE (Lines 1870-1881)

### 3.5 `handleSignUp()`
- **Lines**: 1883-1898
- **Status**: ❌ UNUSED
- **Reason**: Only called from a form that's never triggered. The signup form is in a hidden modal that nothing opens.
- **Recommendation**: ✂️ REMOVE (Lines 1883-1898)

### 3.6 `openServiceStats()`, `closeServiceStats()`, `renderServiceStats()`
- **Lines**: 2899-2977
- **Status**: ❌ UNUSED
- **Reason**: Functions exist but `serviceStatsModal` is never opened. No visible button calls `showServiceStats()`.
- **Recommendation**: ✂️ REMOVE (Lines 2899-2977)

### 3.7 `downloadVerifyQR()`
- **Lines**: 2655-2669
- **Status**: ❌ UNUSED
- **Reason**: Function exists but is never called. The verification display doesn't use it.
- **Recommendation**: ✂️ REMOVE

### 3.8 `printCeremonyCard()` - PARTIAL
- **Lines**: 4029-4088
- **Status**: ⚠️ POSSIBLY UNUSED
- **Reason**: Called from `showDetailsList()` but `showDetailsList()` is never called from the UI
- **Note**: At least `printVisitorCard()` is used in verification
- **Recommendation**: Review if needed or REMOVE

### 3.9 `showDetailsList()`
- **Lines**: 3944-4027
- **Status**: ❌ UNUSED
- **Reason**: Function is defined but never called. The stats boxes on dashboard don't have click handlers.
- **Recommendation**: ✂️ REMOVE

### 3.10 `showVisitorDetails()`
- **Lines**: 3536-3551
- **Status**: ⚠️ QUESTIONABLE
- **Reason**: Called from dashboard visitor items, but shows a browser `alert()` which is poor UX
- **Recommendation**: Consider improving or remove

---

## 4. UNREACHABLE/DEAD CODE BLOCKS 🟡

### 4.1 Authentication Gate System
- **Lines**: 1746-1756
- **Status**: ❌ DEAD CODE
- **Details**:
  - `requireAuth()` function always warns but continues
  - No actual authentication enforcement
  - `authGate` element doesn't exist in HTML
- **Code Affected**:
  ```javascript
  const gate = document.getElementById('authGate'); // authGate doesn't exist
  if (!u) {
    if (gate) gate.style.display = 'flex'; // never happens
    alert('Must be logged in');
    return false;
  }
  ```
- **Recommendation**: ✂️ REMOVE (Lines 1746-1756)

### 4.2 `auth.onAuthStateChanged()` Event Listener
- **Lines**: 1757-1771
- **Status**: ❌ MOSTLY DEAD
- **Reason**: Checks for `authGate` element that doesn't exist. Never enforces authentication.
- **Recommendation**: ✂️ REMOVE or refactor with actual gate element

### 4.3 Duplicate playSound() Function Definition
- **Lines**: 1900-1916 (First definition)
- **Lines**: 3898-3915 (Second definition) 
- **Status**: ❌ REDUNDANT
- **Reason**: Function `playSound()` is defined twice with slightly different logic
- **Details**:
  - First version (1900-1916): More detailed with waveform types
  - Second version (3898-3915): Simpler version
  - Both are identical in purpose
- **Recommendation**: ✂️ REMOVE one definition (keep lines 3898-3915 as it's used later)

### 4.4 Duplicate Daily Report Generation
- **Lines**: 4010-4011 and 4012-4013
- **Status**: ❌ REDUNDANT CODE
- **Details**:
  ```javascript
  document.getElementById('reportContent').innerHTML = '<div class="report-section">...';
  // ... followed immediately by
  document.getElementById('reportContent').innerHTML = '<div class="report-section">...'; // EXACT DUPLICATE
  ```
- **Recommendation**: ✂️ REMOVE one of these (Lines 4012-4013)

---

## 5. UNUSED PROPERTIES & LOCAL VARIABLES 🟣

### 5.1 Unused Visitor Properties
In the `visitor` object created in `createVisitor()`:

- **`requestNumber`** (Line 1983) - Set to empty string, never populated, but displayed
- **`cerPlace`** - Referenced in some display code but should be `place`
- **`serviceStatsCount`** - Referenced but never set

### 5.2 Unused Event Properties
In `mariageEvents` array:
- All events are stored but **never actually displayed or used** in the output
- Lives in memory but not persisted or shown to users
- The events are only added to the object but never rendered (Lines 2477-2503)

### 5.3 Unused Variables in Functions

#### In `showServiceStats()` (Line 2899):
- `countEl` is never actually used to update display

#### In `renderHistorySearchResults()` (Line 3395):
- `endTimeStr` is computed but not always necessary

---

## 6. CONFIGURATION ISSUES 🟠

### 6.1 Broken Modal References
- **signupModal** (Line 1626): Created but never opened from UI
- **serviceStatsModal** (Line 1645): Created but never opened
- The modal structure exists but functionality is orphaned

### 6.2 Incomplete Authentication System
- Google OAuth configured but no button to use it
- Email signup/signin configured but no UI triggers
- Auth state listener implemented but no UI reflects auth state

---

## 7. SUMMARY STATISTICS

| Category | Count | Severity |
|----------|-------|----------|
| Unused Firebase Modules | 3 | 🔴 HIGH |
| Unused Global Variables | 3 | 🔴 HIGH |
| Unused Functions | 12+ | 🔴 HIGH |
| Duplicate Code Blocks | 2 | 🟡 MEDIUM |
| Dead Code Sections | 3 | 🟡 MEDIUM |
| Total Issues | 23+ | |

---

## RECOMMENDED CLEANUP ACTIONS (By Priority)

### CRITICAL - Remove Immediately:
1. **Lines 1844-1848**: Unused Firebase scripts
2. **Lines 1850-1852**: `analytics`, `db`, `storage` variables
3. **Lines 1703-1824**: All unused Auth and Firestore functions
4. **Lines 1921-1922**: `createTabUnlocked`, `ceremonyTabUnlocked`
5. **Line 1868**: `streamActive` variable
6. **Lines 4012-4013**: Duplicate reportContent assignment

### HIGH - Review and Remove:
7. **Lines 1870-1898**: Unused signup/modal functions
8. **Lines 2899-2977**: `openServiceStats` and related functions
9. **Lines 3944-4027**: `showDetailsList()` function
10. **Line 2655-2669**: `downloadVerifyQR()` function
11. **Lines 1703-1771**: Authentication gate system

### MEDIUM - Refactor:
12. Consolidate `playSound()` definitions
13. Remove or refactor `showVisitorDetails()`
14. Complete or remove `printCeremonyCard()` or `showDetailsList()`
15. Verify `mariageEvents` persistence and usage

---

## NOTES FOR DEVELOPER

The application appears to have been refactored from a Firebase backend architecture to a localStorage-only architecture, leaving behind:
- Firebase initialization code that's not actually used
- Authentication functions that were partially implemented
- Database CRUD operations that are now obsolete
- Old password protection attempts that were disabled

**Recommendation**: Complete the server-side integration properly OR completely remove all Firebase-related code for a cleaner codebase.
