# 🧭 TAYYIBFOOD — PRODUCT BLUEPRINT REQUIREMENTS (PBR)

**Version:** 1.0  
**Date:** 2025-11-10  
**Author:** System Architecture Team  
**Project Type:** AI-Powered Progressive Web App (PWA)  
**AI Foundation:** Gemini 2.5 Pro API  
**Prompt Protocol:** PROMPT-NEXUS-8.0  

---

## 1. 🧩 Executive Summary

**TayyibFood** is a mobile-first PWA that empowers users to **analyze the halal compliance of food and cosmetic products** by simply capturing or uploading product images.  
Using **Gemini 2.5 Pro** for OCR and ingredient analysis, the system flags potentially **non-halal** or **doubtful** ingredients and provides transparent explanations.

It merges AI-driven ingredient recognition with a **secure local database** and a **beautiful, user-friendly design**, ensuring privacy, accuracy, and ethical alignment.

---

## 2. 🎯 Vision Statement

> “To enable every consumer to make informed, halal-conscious product choices through intelligent, transparent, and ethical AI technology.”

---

## 3. 🧱 Core Objectives

1. **Halal Risk Detection:** Automatically detect doubtful or non-halal ingredients from images.  
2. **Transparency:** Provide ingredient explanations and risk levels.  
3. **Data Privacy:** Keep all API keys and scan data encrypted locally.  
4. **Accessibility:** Deliver a fast, offline-capable, and mobile-first user experience.  
5. **Scalability:** Prepare for integration with broader food/cosmetic databases and APIs.  

---

## 4. ⚙️ Functional Requirements

### 4.1 Image Input & Processing
- Users can **upload** or **capture** product images.
- Gemini 2.5 Pro API handles OCR and ingredient extraction.
- AI parses extracted text, filters noise, and identifies ingredients.

### 4.2 Ingredient Analysis & Risk Assessment
- Each ingredient is compared against a reference halal database.
- Risk categories:
  - 🟢 **Halal/Safe**
  - 🟡 **Doubtful**
  - 🔴 **Non-Halal**
- Each risk includes:
  - **Confidence score** (0–1)
  - **Explanation** of reasoning
  - **Source reference**

### 4.3 User Data Management
- Local or cloud-based storage of:
  - Product name / brand
  - Scanned ingredients list
  - Risk report (JSON)
  - Timestamp
- API keys stored securely (encrypted with AES).

### 4.4 Alerts & Insights
- Instant alert if any ingredient is flagged as “doubtful” or “non-halal”.
- Optional educational tip: *“Why is this ingredient considered doubtful?”*
- Suggest alternative products or ingredients.

### 4.5 API Key Management
- On first launch: request Gemini API key.
- Securely store and allow easy update from settings.
- Never transmit API key unencrypted.

### 4.6 Offline Capability
- PWA caching system allows last scans to be viewed offline.
- Basic UI accessible even when disconnected.

---

## 5. 🖥️ User Interface Requirements

| Element | Description |
|----------|--------------|
| **Design Style** | Clean, modern, minimalistic, bright accent colors |
| **Primary Layout** | Mobile-first (PWA), responsive grid |
| **Main Screen** | “Scan Product” button, image upload zone |
| **Results Screen** | Ingredient list + color-coded risk levels |
| **Settings Screen** | API key management, preferences, history |
| **Typography** | Sans-serif, medium weight, readable contrast |
| **Color Coding** | Green = Safe, Yellow = Doubtful, Red = Non-halal |

---

## 6. 🤖 AI & Technical Architecture

### 6.1 AI Workflow
1. **Input:** Product image uploaded or captured.
2. **OCR Stage:** Gemini 2.5 extracts text.
3. **Ingredient Parsing:** Text filtered, cleaned, and tokenized.
4. **Halal Risk Check:** Ingredients cross-referenced with known database.
5. **Output:** JSON response with risk analysis and explanations.

### 6.2 System Components
- **Frontend:** PWA (React, Next.js, or Angular)
- **Backend:** Node.js or Spring Boot API
- **AI Model:** Gemini 2.5 Pro (OCR + classification)
- **Database:** Local IndexedDB or remote MongoDB/PostgreSQL
- **Storage:** Encrypted product history cache
- **Authentication:** Local user session or API key-based

### 6.3 API Data Flow
```text
[User Image] 
   ↓
[Gemini 2.5 Pro API]
   ↓ (OCR + ingredient extraction)
[TayyibFood Backend]
   ↓ (classification logic)
[Local DB + Risk JSON]
   ↓
[UI Visualization Layer]
