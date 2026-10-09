# Sections

This file defines all sections, their ordering, impact levels, and descriptions.
The section ID (in parentheses) is the filename prefix used to group rules.

---

## 1. Placement (placement)

**Impact:** CRITICAL  
**Description:** Which top-level folder a piece of code belongs in. Wrong placement spreads one concern across layers.

## 2. Features (feature)

**Impact:** HIGH  
**Description:** How a feature slice is bounded and laid out: by backend domain, then by page or workflow, then by role.

## 3. Naming (naming)

**Impact:** MEDIUM  
**Description:** File names that say what a file is and which feature it belongs to.

## 4. Ownership (ownership)

**Impact:** MEDIUM  
**Description:** Which file owns layout, fields, data loading, and the loaded record.
