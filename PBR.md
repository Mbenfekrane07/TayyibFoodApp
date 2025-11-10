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
| ID    | Objective            | Description                                                                         |
| ----- | -------------------- | ----------------------------------------------------------------------------------- |
| OBJ-1 | Ingredient Scanning  | Enable users to upload or capture an image of food/cosmetic products.               |
| OBJ-2 | OCR & AI Analysis    | Use Gemini 2.5 Pro API to extract ingredients from product labels.                  |
| OBJ-3 | Halal Risk Detection | Classify ingredients as **Safe**, **Doubtful**, or **Non-Halal** with explanations. |
| OBJ-4 | Data Storage         | Store scanned product information and results in a local or cloud DB.               |
| OBJ-5 | Secure API Usage     | Request and store user’s Gemini API key securely (encrypted).                       |
| OBJ-6 | User Experience      | Provide a clean, attractive, mobile-first interface.                                |
| OBJ-7 | Safety & Privacy     | Avoid religious judgments; ensure data security and cultural sensitivity.           |

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

| ID    | Category               | Requirement                                            | Priority |
| ----- | ---------------------- | ------------------------------------------------------ | -------- |
| FR-01 | Image Input            | Allow users to upload or take a product photo.         | High     |
| FR-02 | API Integration        | Use Gemini 2.5 Pro API for OCR + visual parsing.       | High     |
| FR-03 | Ingredient Detection   | Identify ingredients and generate list.                | High     |
| FR-04 | Risk Classification    | Tag ingredients as Safe/Doubtful/Non-Halal.            | High     |
| FR-05 | Result Explanation     | Provide reason and confidence for each tag.            | Medium   |
| FR-06 | Local Storage          | Save previous scans and metadata.                      | High     |
| FR-07 | API Key Management     | Store API key securely (encrypted).                    | High     |
| FR-08 | UI Feedback            | Alert users when a product includes risky ingredients. | High     |
| FR-09 | Multi-Language Support | Support English / Arabic / French.                     | Medium   |
| FR-10 | Educational Insights   | Suggest safer alternatives or notes.                   | Low      |

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

## 5. ⚙️ Non-Functional Requirements
---
| ID     | Type                | Description                                                            | Target     |
| ------ | ------------------- | ---------------------------------------------------------------------- | ---------- |
| NFR-01 | **Performance**     | Scan + analysis should complete in < 5 seconds (on stable connection). | 5s         |
| NFR-02 | **Security**        | Encrypt API key using AES or OS-secure storage.                        | 100%       |
| NFR-03 | **Privacy**         | No personal data sent externally.                                      | 100%       |
| NFR-04 | **Availability**    | PWA must function offline with cached history.                         | 99% uptime |
| NFR-05 | **Accessibility**   | Interface must meet WCAG 2.1 AA standards.                             | Pass       |
| NFR-06 | **Scalability**     | Backend must support at least 10k daily active users.                  | 10k/day    |
| NFR-07 | **Maintainability** | Code modular and documented (SOLID, DRY).                              | ✅          |

## 6. 🖥️ User Interface Requirements

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

## 7. 🤖 AI & Technical Architecture
| Component                       | Description                                                                              |
| ------------------------------- | ---------------------------------------------------------------------------------------- |
| **Frontend (PWA)**              | Built with modern UI (React/Vue/Angular). Mobile-first, responsive, and offline capable. |
| **Backend API Layer**           | Manages user sessions, product scan requests, and database operations.                   |
| **AI Agent (TayyibFood Agent)** | Core intelligent system prompt managing image → ingredient → halal analysis pipeline.    |
| **Gemini 2.5 Pro API**          | External image understanding and OCR model used for ingredient detection.                |
| **Database**                    | Stores scanned results, product metadata, and user configuration securely.               |
| **Encryption Module**           | Ensures safe storage of API keys and user preferences locally.                           |

### 7.1 AI Workflow
1. **Input:** Product image uploaded or captured.
2. **OCR Stage:** Gemini 2.5 extracts text.
3. **Ingredient Parsing:** Text filtered, cleaned, and tokenized.
4. **Halal Risk Check:** Ingredients cross-referenced with known database.
5. **Output:** JSON response with risk analysis and explanations.

### 7.2 System Components
- **Frontend:** PWA (React, Next.js, or Angular)
- **Backend:** Node.js or Spring Boot API
- **AI Model:** Gemini 2.5 Pro (OCR + classification)
- **Database:** Local IndexedDB or remote MongoDB/PostgreSQL
- **Storage:** Encrypted product history cache
- **Authentication:** Local user session or API key-based

### 7.3 API Data Flow
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
```
## 8. 📄 Output Specification

### 7.1 JSON Schema for Scan Results
```json
{
  "productName": "string",
  "brand": "string|null",
  "imageId": "string",
  "ingredients": [
    {
      "name": "string",
      "riskLevel": "Safe | Doubtful | NonHalal",
      "confidence": "float (0-1)",
      "reason": "string"
    }
  ],
  "overallRisk": "Safe | Doubtful | NonHalal",
  "analysisSummary": "string",
  "timestamp": "ISO8601 string",
  "educationalNote": "string"
}
```
