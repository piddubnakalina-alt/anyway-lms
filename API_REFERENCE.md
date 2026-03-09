# 🔌 API Reference

Base URL: `https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b`

## Authentication

All protected endpoints require an Authorization header:
```
Authorization: Bearer <access_token>
```

Get access token from `signIn()` response or stored session.

---

## 🔐 Auth Endpoints

### Sign Up
```http
POST /auth/signup
Content-Type: application/json

{
  "email": "student@example.com",
  "password": "securepassword",
  "metadata": {
    "name": "Student Name",
    "role": "student"
  }
}
```

**Response:**
```json
{
  "success": true,
  "session": {
    "access_token": "eyJ...",
    "user": {
      "id": "uuid",
      "email": "student@example.com",
      "user_metadata": {
        "name": "Student Name",
        "role": "student"
      }
    }
  }
}
```

---

## 📚 Resource Endpoints

### Get All Resources
```http
GET /resources
```

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "resource:123",
      "title": "Present Simple Quiz",
      "type": "pdf",
      "url": "https://...",
      "category": "grammar",
      "level": "A1",
      "description": "...",
      "assignedStudents": ["student:456", "all"],
      "createdAt": "2024-01-01T00:00:00Z",
      "createdBy": "teacher:789"
    }
  ]
}
```

### Get Resources by Student
```http
GET /resources/student/:studentId
```

### Create Resource
```http
POST /resources
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "New Material",
  "type": "pdf",
  "url": "https://drive.google.com/...",
  "category": "grammar",
  "level": "A2",
  "description": "Description here",
  "assignedStudents": ["student:123", "all"],
  "fileName": "material.pdf",
  "fileSize": 1024000,
  "storagePath": "user123/material.pdf"
}
```

### Update Resource
```http
PUT /resources/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Updated Title",
  "assignedStudents": ["student:456"]
}
```

### Delete Resource
```http
DELETE /resources/:id
Authorization: Bearer <token>
```

---

## 👥 Student Endpoints

### Get All Students
```http
GET /students
```

### Get Student by ID
```http
GET /students/:id
```

### Create Student
```http
POST /students
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "level": "B1",
  "age": 25,
  "goals": "Travel and work abroad",
  "lessonsCompleted": 0,
  "nextLesson": "2024-01-15T10:00:00Z"
}
```

### Update Student
```http
PUT /students/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "level": "B2",
  "lessonsCompleted": 12
}
```

### Delete Student
```http
DELETE /students/:id
Authorization: Bearer <token>
```

---

## 📊 Progress Endpoints

### Get All Progress
```http
GET /progress
```

### Get Progress by Student
```http
GET /progress/student/:studentId
```

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "progress:resource123:student456",
      "resourceId": "resource:123",
      "studentId": "student:456",
      "completed": true,
      "completedAt": "2024-01-10T15:30:00Z"
    }
  ]
}
```

### Mark Resource Complete/Incomplete
```http
POST /progress
Authorization: Bearer <token>
Content-Type: application/json

{
  "resourceId": "resource:123",
  "studentId": "student:456",
  "completed": true
}
```

---

## 📖 Vocabulary Endpoints

### Get Vocabulary by Student
```http
GET /vocabulary/student/:studentId
```

### Add Vocabulary Word
```http
POST /vocabulary
Authorization: Bearer <token>
Content-Type: application/json

{
  "studentId": "student:123",
  "word": "hello",
  "translation": "привіт",
  "example": "Hello, how are you?",
  "category": "greetings",
  "mastered": false
}
```

### Update Vocabulary Word
```http
PUT /vocabulary/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "mastered": true,
  "lastReviewed": "2024-01-10T15:00:00Z"
}
```

### Delete Vocabulary Word
```http
DELETE /vocabulary/:id
Authorization: Bearer <token>
```

---

## 💬 Testimonial Endpoints

### Get All Testimonials
```http
GET /testimonials
```

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "testimonial:123",
      "name": "Student Name",
      "text": "Great teacher!",
      "rating": 5,
      "level": "B1",
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ]
}
```

### Create Testimonial
```http
POST /testimonials
Content-Type: application/json

{
  "name": "Student Name",
  "text": "Excellent platform and teacher!",
  "rating": 5,
  "level": "B2"
}
```

---

## 💰 Pricing Endpoints

### Get Pricing
```http
GET /pricing
```

**Response:**
```json
{
  "success": true,
  "data": {
    "individual": {
      "trial": { "price": 300, "duration": "60 хвилин" },
      "single": { "price": 500, "duration": "60 хвилин" },
      "package4": { "price": 1800, "pricePerLesson": 450, "lessons": 4 }
    },
    "group": {
      "single": { "price": 300, "duration": "60 хвилин" }
    },
    "currency": "грн"
  }
}
```

### Update Pricing
```http
PUT /pricing
Authorization: Bearer <token>
Content-Type: application/json

{
  "individual": {
    "trial": { "price": 350, "duration": "60 хвилин" }
  },
  "currency": "грн"
}
```

---

## 📋 Policy Endpoints

### Get Policy
```http
GET /policy
```

**Response:**
```json
{
  "success": true,
  "data": {
    "cancellation": {
      "advance": "24 години",
      "penalty": "Заняття вважається проведеним"
    },
    "payment": {
      "methods": ["Готівка", "Картка"],
      "terms": "Оплата до початку пакету"
    }
  }
}
```

### Update Policy
```http
PUT /policy
Authorization: Bearer <token>
Content-Type: application/json

{
  "cancellation": {
    "advance": "48 години",
    "penalty": "50% вартості"
  }
}
```

---

## 📦 Storage API

### Upload File
```javascript
import { uploadFile } from './lib/storage';

const file = event.target.files[0];
const userId = currentUser.id;

const result = await uploadFile(file, userId);

if (result.success) {
  console.log('URL:', result.url);
  console.log('Path:', result.path);
}
```

**Result:**
```json
{
  "success": true,
  "url": "https://xukykdgkzerkeygxbmhm.supabase.co/storage/v1/object/public/make-e9e9da7b-resources/user123/file.pdf",
  "path": "user123/file.pdf"
}
```

### Delete File
```javascript
import { deleteFile } from './lib/storage';

const result = await deleteFile('user123/file.pdf');
```

---

## 🛡️ Error Handling

All endpoints return consistent error format:

```json
{
  "success": false,
  "error": "Error message describing what went wrong"
}
```

### Common HTTP Status Codes

- `200` - Success
- `400` - Bad Request (invalid data)
- `401` - Unauthorized (missing/invalid token)
- `404` - Not Found
- `500` - Internal Server Error

### Example Error Response

```json
{
  "success": false,
  "error": "Resource not found"
}
```

---

## 🔍 Data Types

### ResourceType
```typescript
type ResourceType = "pdf" | "audio" | "video" | "link";
```

### ResourceCategory
```typescript
type ResourceCategory = "homework" | "reading" | "grammar" | "vocabulary" | "video";
```

### ResourceLevel
```typescript
type ResourceLevel = "A0" | "A1" | "A2" | "B1" | "B2" | "C1" | "C2" | "All";
```

### Resource Object
```typescript
interface Resource {
  id: string;
  title: string;
  type: ResourceType;
  url: string;
  category: ResourceCategory;
  level: ResourceLevel;
  description?: string;
  assignedStudents: string[]; // ["student:123", "all"]
  createdAt: string; // ISO date
  createdBy: string; // user ID
  fileName?: string;
  fileSize?: number;
  storagePath?: string;
}
```

---

## 💻 Code Examples

### Frontend API Usage

```typescript
import * as api from './lib/api';

// Fetch resources
const { success, data, error } = await api.fetchResources();
if (success) {
  console.log('Resources:', data);
}

// Create resource
const result = await api.createResource({
  title: "New Material",
  type: "pdf",
  url: "https://...",
  category: "grammar",
  level: "A1",
  assignedStudents: ["all"]
});

// Update progress
await api.updateProgress("resource:123", "student:456", true);
```

### Authentication Flow

```typescript
import { signIn, storeSession, getCurrentUser } from './lib/supabase-auth';

// Sign in
const result = await signIn(email, password);
if (result.success && result.session) {
  storeSession(result.session);
  
  // Get current user
  const user = getCurrentUser();
  console.log('Logged in as:', user.email);
}
```

---

## 🧪 Testing

### Health Check
```bash
curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/health
```

### Get Resources (No Auth)
```bash
curl https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/resources
```

### Create Resource (With Auth)
```bash
curl -X POST \
  https://xukykdgkzerkeygxbmhm.supabase.co/functions/v1/make-server-e9e9da7b/resources \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Test Material",
    "type": "pdf",
    "url": "https://example.com/test.pdf",
    "category": "grammar",
    "level": "A1",
    "assignedStudents": ["all"]
  }'
```

---

**Happy Coding! 🚀**
