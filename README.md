# Privacy-Preserving Document Verification using Zero-Knowledge Proofs

A research project that enables users to prove specific facts about their documents without revealing the original document or unnecessary sensitive information.

---

## Project Overview

Traditional document verification requires users to share complete documents, exposing sensitive personal information such as names, dates of birth, addresses, identification numbers, and academic records.

This project uses **Zero-Knowledge Proofs (ZKPs)** to allow users to prove selected claims about a document while keeping the original document private.

The system combines:

- OCR-based document processing
- Attribute extraction
- Document type detection
- Claim selection
- Circom circuits
- Witness generation
- Groth16 proof generation
- Cryptographic proof verification
- Frontend and backend integration

The primary objective is **privacy-preserving and selective document verification**.

---

## Problem Statement

In conventional document verification systems:

- Complete documents must often be shared.
- Sensitive personal information is exposed unnecessarily.
- Verifiers gain access to information unrelated to the requested verification.
- Data minimization becomes difficult.

For example, suppose a verifier only wants to confirm:

> **Age ≥ 18**

A conventional verification process may require the user to share an entire identity document containing:

- Full name
- Date of birth
- Address
- Identification number
- Other personal information

This exposes significantly more information than is required.

---

## Proposed Solution

The proposed system uses Zero-Knowledge Proofs to allow a user to prove a selected claim without directly sharing the original document with the verifier.

The general workflow is:

1. Upload a supported document.
2. Process the document using OCR or text extraction.
3. Detect the document type.
4. Extract relevant attributes.
5. Select a verification claim.
6. Generate circuit inputs.
7. Generate a witness.
8. Generate a Groth16 Zero-Knowledge Proof.
9. Download or share the generated proof artifacts.
10. Allow another party to independently verify the proof.

The verifier can cryptographically determine whether the claim is valid without requiring the original document.

---

## Key Features

### Privacy-Preserving Verification

Verify selected document attributes without requiring the verifier to access the complete original document.

### OCR-Based Processing

The system supports document processing and information extraction from supported formats including:

- PDF
- Images
- DOCX
- Text files

### Document Type Detection

The system identifies the type of document and selects the appropriate processing and verification logic.

### Attribute Extraction

Relevant attributes are extracted from the processed document before generating the Zero-Knowledge Proof.

### Claim-Based Verification

Users can select specific claims instead of proving or revealing the entire document.

### Zero-Knowledge Proof Generation

The system generates cryptographic proof artifacts using Circom and SnarkJS with the Groth16 proving system.

Generated artifacts include:

- `proof.json`
- `public.json`
- `verification_key.json`

### Independent Verification

Generated proofs can be verified independently using the corresponding public signals and verification key.

### Multi-Attribute Verification

The system supports verification of multiple attributes using dedicated multi-attribute circuits.

### Proof Download

Generated proof artifacts can be downloaded for later verification or sharing.

### QR-Based Proof Handling

The frontend includes QR-based functionality for handling proof information.

---

## Supported Verification Claims

### Aadhaar Documents

The system includes circuits and processing support for:

- Name Verification
- Age ≥ 18 Verification
- Gender Verification
- Multi-Attribute Verification

### Academic Documents

The system includes support for:

- Student Name Verification
- Result Verification
- Grade Verification
- Grand Total Verification
- Multi-Attribute Verification

The exact claims available depend on the detected document type and the corresponding circuit configuration.

---

## System Workflow

### Prover Workflow

```text
Upload Document
       ↓
Document Processing
       ↓
OCR / Text Extraction
       ↓
Document Type Detection
       ↓
Attribute Extraction
       ↓
Claim Selection
       ↓
Input Generation
       ↓
Witness Generation
       ↓
Groth16 Proof Generation
       ↓
Proof Artifact Generation
       ↓
Download / Share Proof
```

### Verifier Workflow

```text
Receive Proof Artifacts
       ↓
Upload Proof
       ↓
Load Public Signals
       ↓
Load Verification Key
       ↓
Cryptographic Verification
       ↓
VALID / INVALID PROOF
```

---

## System Architecture

```text
                         ┌─────────────────────┐
                         │    User Document    │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │ Document Processing │
                         │ OCR / Text Extract  │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │  Document Type      │
                         │     Detection       │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │ Attribute Extraction│
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │   Claim Selection   │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │   Input Generation  │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │   Circom Circuit    │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │ Witness Generation  │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │ Groth16 Proof       │
                         │    Generation       │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │   Proof Artifact    │
                         │     Generation      │
                         └──────────┬──────────┘
                                    │
                                    ↓
                         ┌─────────────────────┐
                         │ Proof Verification  │
                         └─────────────────────┘
```

---

## Technology Stack

### Frontend

- React
- TypeScript
- Vite
- Tailwind CSS
- Framer Motion

### Backend

- Node.js
- Express.js
- Multer

### Zero-Knowledge Proofs

- Circom
- SnarkJS
- Groth16
- Poseidon Hash

### OCR and Document Processing

- Tesseract OCR
- PDF parsing
- DOCX extraction
- Image processing
- Text extraction

### Development Environment

- Windows
- Ubuntu / WSL
- Node.js
- Git
- GitHub

---

## Project Structure

```text
ZKP-DOCVerify
│
├── backend
│   ├── issuer
│   │   ├── generateKeys.js
│   │   ├── issuerConfig.js
│   │   ├── signDocument.js
│   │   └── test-authenticity.js
│   │
│   ├── middleware
│   │   └── errorHandler.js
│   │
│   ├── routes
│   │   ├── authenticityVerifier.js
│   │   ├── download.js
│   │   ├── generateProof.js
│   │   ├── getProof.js
│   │   ├── health.js
│   │   ├── ocr.js
│   │   ├── upload.js
│   │   └── verifyProof.js
│   │
│   ├── services
│   │   ├── proofMutex.js
│   │   └── proofStore.js
│   │
│   ├── zk-document-verification
│   │   ├── circuits
│   │   ├── config
│   │   ├── extractors
│   │   ├── processors
│   │   ├── samples
│   │   ├── verification keys
│   │   └── main.js
│   │
│   ├── package.json
│   └── server.js
│
├── frontend
│   └── zkp-verify
│       ├── src
│       │   ├── components
│       │   ├── config
│       │   ├── content
│       │   ├── context
│       │   ├── hooks
│       │   ├── layouts
│       │   ├── lib
│       │   ├── pages
│       │   ├── routes
│       │   ├── services
│       │   └── utils
│       │
│       ├── package.json
│       ├── tsconfig.json
│       └── vite.config.ts
│
├── .gitignore
├── README.md
└── vercel.json
```

---

## Installation

### Clone Repository

Navigate into the project:

```bash
cd zkp-document-verification
```

---

## Backend Setup

Navigate to the backend:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

Start the backend server:

```bash
node server.js
```

The backend server runs locally according to the configured server port.

---

## Frontend Setup

Open another terminal and navigate to:

```bash
cd frontend/zkp-verify
```

Install dependencies:

```bash
npm install
```

Start the frontend development server:

```bash
npm run dev
```

The Vite development server will provide the local frontend URL in the terminal.

---

## ZKP Engine Setup

Navigate to the ZKP engine:

```bash
cd backend/zk-document-verification
```

Install dependencies:

```bash
npm install
```

The ZKP engine contains the Circom circuits, input generators, witness generation logic, proof generation logic, and verification logic.

---

## Verify ZKP Installation

Check Circom:

```bash
circom --version
```

Check SnarkJS:

```bash
snarkjs --version
```

Both tools should be available in the development environment before compiling or generating proofs.

---

## Usage

### Generate a Proof

1. Open the frontend application.
2. Navigate to the **Generate Proof** page.
3. Upload a supported document.
4. Allow the system to process the document.
5. Review the extracted information.
6. Select the verification claim.
7. Generate the circuit inputs.
8. Generate the witness.
9. Generate the Zero-Knowledge Proof.
10. Download the generated proof artifacts.

The generated artifacts include:

```text
proof.json
public.json
verification_key.json
```

---

## Verify a Proof

1. Open the **Verify Proof** page.
2. Upload the generated proof.
3. Upload the corresponding public signals.
4. Upload the verification key.
5. Click **Verify Proof**.
6. The system performs cryptographic verification.
7. The result is displayed as either a valid or invalid proof.

Example successful result:

```text
✓ VALID PROOF

This proof is cryptographically valid.
```

Example failed result:

```text
✗ INVALID PROOF

This proof failed cryptographic verification.
```

---

## Zero-Knowledge Proof Process

The Zero-Knowledge Proof pipeline follows these stages:

```text
Document
   ↓
Extract Attributes
   ↓
Select Claim
   ↓
Generate Circuit Inputs
   ↓
Witness Generation
   ↓
Groth16 Proving
   ↓
Proof + Public Signals
   ↓
Cryptographic Verification
```

The private document information is used during the proving process, while the verifier receives the proof artifacts required for cryptographic verification.

---

## Security and Privacy

The system is designed around the principle of **Selective Disclosure**.

The objective is to minimize the amount of sensitive information that must be shared during verification.

### Private Information

The following information is intended to remain with the prover:

- Original document
- Raw OCR text
- Sensitive personal details
- Private document attributes
- Private circuit inputs

### Shared Information

The verifier receives the cryptographic proof artifacts required for verification, such as:

- Zero-Knowledge Proof
- Public Signals
- Verification Key

This enables a verifier to determine whether the selected claim is satisfied without requiring direct access to the original document.

---

## Example Use Case

Consider an identity document containing:

```text
Name: Example User
Date of Birth: 01/01/2000
Address: Example Address
Identification Number: XXXXXXXX
```

A verifier may only need to know whether the individual is at least 18 years old.

Instead of sharing the complete document, the system can generate a Zero-Knowledge Proof for the claim:

```text
Age ≥ 18
```

The verifier can then verify the proof without receiving the complete identity document.

This demonstrates the principle of **minimum disclosure**.

---

##  Contribution

This project demonstrates the application of Zero-Knowledge Proofs to privacy-preserving document verification.

The implementation integrates multiple components into an end-to-end workflow:

- Document processing
- OCR
- Attribute extraction
- Document type detection
- Claim selection
- Circuit input generation
- Circom circuit design
- Witness generation
- Groth16 proof generation
- Cryptographic proof verification
- Frontend and backend integration

The project demonstrates how ZKPs can reduce unnecessary exposure of sensitive information while still allowing a verifier to establish the validity of a selected claim.

---

## Future Scope

Potential future improvements include:

- Additional document types
- PAN card verification
- Passport verification
- Degree certificate verification
- Blockchain integration
- Smart contract-based verification
- Decentralized proof storage
- Mobile application support
- Additional document attributes
- More complex multi-attribute claims
- Issuer-based document authenticity verification
- Improved OCR accuracy
- Distributed verification infrastructure

---


## Limitations

The current implementation depends on accurate document processing and attribute extraction.

OCR-based extraction may be affected by:

- Image quality
- Document orientation
- Font styles
- Blurred documents
- Complex layouts
- Incorrectly detected text

The generated proof also depends on the correctness of the configured circuit and its corresponding proving and verification artifacts.

---

## Development

The project is organized into separate frontend, backend, and Zero-Knowledge Proof components.

### Frontend

The frontend provides the user interface for:

- Document upload
- Claim selection
- Proof generation
- Proof downloading
- Proof verification
- Verification history
- Navigation and workflow presentation

### Backend

The backend provides APIs for:

- Document upload
- OCR processing
- Proof generation
- Proof retrieval
- Proof verification
- Download operations
- Health checks
- Authenticity verification

### ZKP Engine

The ZKP engine provides:

- Document extraction
- Attribute extraction
- Claim generation
- Input generation
- Circuit selection
- Circuit compilation
- Witness generation
- Groth16 proof generation
- Proof verification

