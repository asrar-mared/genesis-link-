# 🔌 API DOCUMENTATION - توثيق واجهة البرمجة

<div align="center">

**Genesis Link - RESTful API v1**

[![API Version](https://img.shields.io/badge/API-v1.0.0-blue.svg)](https://api.genesislink.io)
[![Status](https://img.shields.io/badge/Status-Stable-success.svg)](https://status.genesislink.io)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0-green.svg)](https://api.genesislink.io/docs)

> 📚 **دليل شامل لجميع نقاط النهاية (Endpoints)**  
> توثيق كامل، أمثلة عملية، وأفضل الممارسات

[🚀 Quick Start](#-quick-start) • [🔐 Authentication](#-authentication) • [📡 Endpoints](#-endpoints) • [💡 Examples](#-code-examples)

</div>

---

## 📋 جدول المحتويات

- [🎯 نظرة عامة](#-نظرة-عامة)
- [🚀 Quick Start](#-quick-start)
- [🔐 Authentication](#-authentication)
- [📡 Endpoints](#-endpoints)
  - [Authentication](#authentication-endpoints)
  - [Users](#users-endpoints)
  - [Threats](#threats-endpoints)
  - [Reports](#reports-endpoints)
  - [Analytics](#analytics-endpoints)
  - [Contributions](#contributions-endpoints)
- [📊 Data Models](#-data-models)
- [⚠️ Error Handling](#️-error-handling)
- [🔄 Pagination](#-pagination)
- [⚡ Rate Limiting](#-rate-limiting)
- [💡 Code Examples](#-code-examples)
- [🧪 Testing](#-testing)
- [📦 SDKs](#-sdks)

---

## 🎯 نظرة عامة

### Base URL

```
Production:  https://api.genesislink.io/v1
Staging:     https://api-staging.genesislink.io/v1
Development: http://localhost:5000/api/v1
```

### API Design Principles

```
✅ RESTful Architecture
✅ JSON Request/Response
✅ JWT Authentication
✅ Versioned APIs (/v1, /v2)
✅ HTTPS Only (Production)
✅ Rate Limited
✅ Comprehensive Error Messages
```

### API Features

| Feature | Description |
|---------|-------------|
| 🔐 **Authentication** | JWT tokens, API keys, OAuth 2.0 |
| 📊 **Pagination** | Cursor & offset-based pagination |
| 🔍 **Filtering** | Query parameters for filtering |
| 📈 **Sorting** | Sort by any field |
| ⚡ **Rate Limiting** | 100 requests/minute |
| 🌐 **CORS** | Configurable origins |
| 📝 **Versioning** | URL-based versioning |
| 🔔 **Webhooks** | Real-time event notifications |

---

## 🚀 Quick Start

### 1. Get API Key

```bash
# Register and get your API key
curl -X POST https://api.genesislink.io/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "cyber_warrior",
    "email": "warrior@example.com",
    "password": "SecurePass123!"
  }'

# Response
{
  "user_id": "user_123abc",
  "api_key": "gl_live_abc123...",
  "message": "Registration successful"
}
```

### 2. Make Your First Request

```bash
# Get all threats
curl -X GET https://api.genesislink.io/v1/threats \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json"
```

### 3. Interactive API Documentation

```
Swagger UI: https://api.genesislink.io/docs
ReDoc:      https://api.genesislink.io/redoc
Postman:    https://www.postman.com/genesislink/workspace
```

---

## 🔐 Authentication

### Authentication Methods

Genesis Link API supports three authentication methods:

#### 1️⃣ JWT Token (Recommended)

```bash
# Login to get JWT token
POST /api/v1/auth/login
Content-Type: application/json

{
  "username": "cyber_warrior",
  "password": "SecurePass123!"
}

# Response
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 1800
}

# Use token in subsequent requests
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

#### 2️⃣ API Key

```bash
# Use API key in header
X-API-Key: gl_live_abc123xyz456...

# Or as query parameter (not recommended for production)
GET /api/v1/threats?api_key=gl_live_abc123xyz456...
```

#### 3️⃣ OAuth 2.0

```bash
# Redirect user to authorization URL
GET /api/v1/oauth/authorize?
  client_id=YOUR_CLIENT_ID&
  redirect_uri=YOUR_CALLBACK_URL&
  response_type=code&
  scope=read:threats write:threats

# Exchange code for token
POST /api/v1/oauth/token
Content-Type: application/json

{
  "grant_type": "authorization_code",
  "code": "AUTH_CODE",
  "client_id": "YOUR_CLIENT_ID",
  "client_secret": "YOUR_CLIENT_SECRET",
  "redirect_uri": "YOUR_CALLBACK_URL"
}
```

---

## 📡 Endpoints

### Authentication Endpoints

#### `POST /auth/register`

Register a new user account.

**Request:**
```json
{
  "username": "cyber_warrior",
  "email": "warrior@example.com",
  "password": "SecurePass123!",
  "full_name": "Cyber Warrior",
  "role": "contributor"
}
```

**Response:** `201 Created`
```json
{
  "user_id": "user_123abc",
  "username": "cyber_warrior",
  "email": "warrior@example.com",
  "api_key": "gl_live_abc123...",
  "created_at": "2025-01-15T10:00:00Z"
}
```

**Errors:**
- `400` - Validation error
- `409` - Username/email already exists

---

#### `POST /auth/login`

Authenticate and receive JWT tokens.

**Request:**
```json
{
  "username": "cyber_warrior",
  "password": "SecurePass123!"
}
```

**Response:** `200 OK`
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 1800,
  "user": {
    "user_id": "user_123abc",
    "username": "cyber_warrior",
    "role": "contributor"
  }
}
```

**Errors:**
- `401` - Invalid credentials
- `429` - Too many login attempts

---

#### `POST /auth/refresh`

Refresh an expired access token.

**Request:**
```json
{
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response:** `200 OK`
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 1800
}
```

---

#### `POST /auth/logout`

Invalidate current session.

**Headers:**
```
Authorization: Bearer YOUR_TOKEN
```

**Response:** `200 OK`
```json
{
  "message": "Successfully logged out"
}
```

---

### Users Endpoints

#### `GET /users/me`

Get current authenticated user profile.

**Headers:**
```
Authorization: Bearer YOUR_TOKEN
```

**Response:** `200 OK`
```json
{
  "user_id": "user_123abc",
  "username": "cyber_warrior",
  "email": "warrior@example.com",
  "profile": {
    "full_name": "Cyber Warrior",
    "avatar_url": "https://cdn.genesislink.io/avatars/...",
    "bio": "Security researcher and bug hunter",
    "location": "Egypt",
    "website": "https://example.com"
  },
  "stats": {
    "contributions": 42,
    "points": 1337,
    "rank": "Elite Defender",
    "badges": [
      {
        "id": "first_contribution",
        "name": "First Contribution",
        "icon": "🎯",
        "earned_at": "2025-01-01T10:00:00Z"
      }
    ]
  },
  "created_at": "2025-01-01T00:00:00Z",
  "last_login": "2025-01-15T10:00:00Z"
}
```

---

#### `PATCH /users/me`

Update current user profile.

**Request:**
```json
{
  "profile": {
    "full_name": "Updated Name",
    "bio": "Updated bio",
    "location": "Cairo, Egypt"
  },
  "settings": {
    "notifications": true,
    "email_digest": "weekly"
  }
}
```

**Response:** `200 OK`
```json
{
  "message": "Profile updated successfully",
  "user": { ... }
}
```

---

#### `GET /users/{user_id}`

Get public user profile.

**Response:** `200 OK`
```json
{
  "user_id": "user_123abc",
  "username": "cyber_warrior",
  "profile": {
    "full_name": "Cyber Warrior",
    "avatar_url": "...",
    "bio": "...",
    "location": "Egypt"
  },
  "stats": {
    "contributions": 42,
    "points": 1337,
    "rank": "Elite Defender"
  },
  "joined_at": "2025-01-01T00:00:00Z"
}
```

---

### Threats Endpoints

#### `GET /threats`

List all threats with filtering and pagination.

**Query Parameters:**

| Parameter | Type | Description | Default |
|-----------|------|-------------|---------|
| `page` | integer | Page number | 1 |
| `per_page` | integer | Items per page (max 100) | 20 |
| `severity` | string | Filter by severity: `low`, `medium`, `high`, `critical` | all |
| `status` | string | Filter by status: `reported`, `confirmed`, `fixed`, `closed` | all |
| `category` | string | Filter by category | all |
| `sort_by` | string | Sort field: `created_at`, `severity`, `title` | created_at |
| `order` | string | Sort order: `asc`, `desc` | desc |
| `search` | string | Search in title/description | - |

**Example Request:**
```bash
GET /api/v1/threats?severity=critical&status=confirmed&per_page=10
```

**Response:** `200 OK`
```json
{
  "threats": [
    {
      "threat_id": "THREAT-2025-001",
      "title": "Critical SQL Injection in Auth Module",
      "description": "SQL injection vulnerability discovered...",
      "severity": "critical",
      "status": "confirmed",
      "category": "web_security",
      "cvss": {
        "score": 9.8,
        "vector": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
        "severity": "CRITICAL"
      },
      "discovered_by": {
        "user_id": "user_123abc",
        "username": "cyber_warrior"
      },
      "created_at": "2025-01-10T10:00:00Z",
      "updated_at": "2025-01-10T14:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "per_page": 10,
    "total": 42,
    "pages": 5,
    "has_next": true,
    "has_prev": false,
    "next_page": "/api/v1/threats?page=2&per_page=10",
    "prev_page": null
  }
}
```

---

#### `POST /threats`

Report a new security threat.

**Request:**
```json
{
  "title": "SQL Injection in Login Form",
  "description": "Discovered SQL injection vulnerability in the authentication module that allows bypassing login checks...",
  "severity": "critical",
  "category": "web_security",
  "tags": ["sql_injection", "authentication", "critical"],
  "technical_details": {
    "affected_component": "app/api/v1/auth.py",
    "vulnerable_code": "query = f\"SELECT * FROM users WHERE username = '{username}'\"",
    "exploit_scenario": "An attacker can inject SQL code...",
    "proof_of_concept": "username: admin' OR '1'='1"
  },
  "affected_versions": ["1.0.0", "1.0.1"],
  "references": [
    "https://cwe.mitre.org/data/definitions/89.html"
  ]
}
```

**Response:** `201 Created`
```json
{
  "threat_id": "THREAT-2025-042",
  "status": "reported",
  "message": "Threat reported successfully",
  "url": "/api/v1/threats/THREAT-2025-042",
  "github_issue": {
    "number": 123,
    "url": "https://github.com/genesislink/genesis-link/issues/123"
  },
  "created_at": "2025-01-15T10:30:00Z"
}
```

**Validation Rules:**
- `title`: Required, 10-200 characters
- `description`: Required, minimum 50 characters
- `severity`: Required, one of: `low`, `medium`, `high`, `critical`
- `category`: Required
- `technical_details`: Optional but recommended

**Errors:**
- `400` - Validation error
- `401` - Unauthorized
- `429` - Rate limit exceeded

---

#### `GET /threats/{threat_id}`

Get detailed information about a specific threat.

**Response:** `200 OK`
```json
{
  "threat_id": "THREAT-2025-001",
  "title": "Critical SQL Injection in Auth Module",
  "description": "SQL injection vulnerability discovered...",
  "severity": "critical",
  "status": "confirmed",
  "category": "web_security",
  "tags": ["sql_injection", "authentication", "critical"],
  "technical_details": {
    "affected_component": "app/api/v1/auth.py",
    "vulnerable_code": "...",
    "exploit_scenario": "...",
    "proof_of_concept": "..."
  },
  "cvss": {
    "score": 9.8,
    "vector": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
    "severity": "CRITICAL"
  },
  "discovered_by": {
    "user_id": "user_123abc",
    "username": "cyber_warrior",
    "profile_url": "/api/v1/users/user_123abc"
  },
  "timeline": [
    {
      "status": "reported",
      "timestamp": "2025-01-10T10:00:00Z",
      "note": "Initial report submitted",
      "updated_by": "user_123abc"
    },
    {
      "status": "confirmed",
      "timestamp": "2025-01-10T14:00:00Z",
      "note": "Vulnerability confirmed by security team",
      "updated_by": "security_team"
    }
  ],
  "affected_versions": ["1.0.0", "1.0.1", "1.1.0"],
  "fixed_in_version": "1.1.1",
  "references": [
    "https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2025-1234",
    "https://github.com/genesislink/genesis-link/security/advisories/..."
  ],
  "related_threats": [
    {
      "threat_id": "THREAT-2025-002",
      "title": "XSS in Comment Section",
      "severity": "high"
    }
  ],
  "created_at": "2025-01-10T10:00:00Z",
  "updated_at": "2025-01-10T14:00:00Z"
}
```

**Errors:**
- `404` - Threat not found

---

#### `PATCH /threats/{threat_id}`

Update threat information (requires permissions).

**Request:**
```json
{
  "status": "confirmed",
  "cvss": {
    "score": 9.8,
    "vector": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H"
  },
  "fixed_in_version": "1.1.1",
  "note": "Fix implemented and tested"
}
```

**Response:** `200 OK`
```json
{
  "message": "Threat updated successfully",
  "threat": { ... },
  "updated_at": "2025-01-15T10:30:00Z"
}
```

**Permissions:**
- Own threats: Can update description, technical details
- Maintainers: Can update status, CVSS, fixed version
- Admins: Full access

---

#### `DELETE /threats/{threat_id}`

Delete a threat report (admin only).

**Response:** `204 No Content`

**Errors:**
- `403` - Forbidden (insufficient permissions)
- `404` - Threat not found

---

### Reports Endpoints

#### `GET /reports`

List all security reports.

**Query Parameters:**
- `type`: Filter by report type (`vulnerability`, `incident`, `audit`, `analysis`)
- `page`, `per_page`: Pagination
- `sort_by`: Sort field
- `published`: Filter published reports only

**Response:** `200 OK`
```json
{
  "reports": [
    {
      "report_id": "RPT-2025-001",
      "type": "security_audit",
      "title": "Monthly Security Audit - January 2025",
      "summary": {
        "total_threats": 12,
        "critical": 2,
        "high": 4,
        "medium": 5,
        "low": 1
      },
      "generated_by": {
        "user_id": "system",
        "automation": true
      },
      "format": "pdf",
      "file_url": "https://s3.genesislink.io/reports/RPT-2025-001.pdf",
      "published": true,
      "created_at": "2025-01-31T23:59:59Z"
    }
  ],
  "pagination": { ... }
}
```

---

#### `POST /reports`

Generate a new security report.

**Request:**
```json
{
  "type": "vulnerability",
  "title": "Q1 2025 Vulnerability Assessment",
  "threat_ids": ["THREAT-2025-001", "THREAT-2025-002"],
  "format": "pdf",
  "include_recommendations": true
}
```

**Response:** `202 Accepted`
```json
{
  "report_id": "RPT-2025-042",
  "status": "generating",
  "message": "Report generation started",
  "estimated_time": "5 minutes",
  "status_url": "/api/v1/reports/RPT-2025-042/status"
}
```

---

#### `GET /reports/{report_id}`

Get report details and download link.

**Response:** `200 OK`
```json
{
  "report_id": "RPT-2025-001",
  "type": "security_audit",
  "title": "Monthly Security Audit - January 2025",
  "summary": {
    "total_threats": 12,
    "critical": 2,
    "high": 4,
    "medium": 5,
    "low": 1
  },
  "findings": [
    {
      "id": 1,
      "title": "SQL Injection Vulnerability",
      "severity": "critical",
      "description": "...",
      "recommendation": "..."
    }
  ],
  "recommendations": [
    "Implement input validation",
    "Use parameterized queries",
    "Enable WAF protection"
  ],
  "metrics": {
    "scan_duration": "2h 30m",
    "files_analyzed": 1500,
    "lines_of_code": 45000,
    "issues_found": 12
  },
  "format": "pdf",
  "file_url": "https://s3.genesislink.io/reports/RPT-2025-001.pdf",
  "file_size": "2.5 MB",
  "download_url": "/api/v1/reports/RPT-2025-001/download",
  "published": true,
  "created_at": "2025-01-31T23:59:59Z"
}
```

---

#### `GET /reports/{report_id}/download`

Download report file.

**Response:** `200 OK`
```
Content-Type: application/pdf
Content-Disposition: attachment; filename="RPT-2025-001.pdf"

[PDF Binary Data]
```

---

### Analytics Endpoints

#### `GET /analytics/overview`

Get overall security analytics and statistics.

**Query Parameters:**
- `period`: Time period (`day`, `week`, `month`, `year`, `all`)
- `start_date`: Start date (ISO 8601)
- `end_date`: End date (ISO 8601)

**Response:** `200 OK`
```json
{
  "period": "month",
  "date_range": {
    "start": "2025-01-01T00:00:00Z",
    "end": "2025-01-31T23:59:59Z"
  },
  "threats": {
    "total": 42,
    "by_severity": {
      "critical": 5,
      "high": 12,
      "medium": 18,
      "low": 7
    },
    "by_status": {
      "reported": 10,
      "investigating": 8,
      "confirmed": 15,
      "fixed": 7,
      "closed": 2
    },
    "by_category": {
      "web_security": 20,
      "api_security": 10,
      "infrastructure": 7,
      "other": 5
    }
  },
  "trends": {
    "threats_per_day": [
      {"date": "2025-01-01", "count": 2},
      {"date": "2025-01-02", "count": 3}
    ],
    "severity_trend": "increasing",
    "most_common_category": "web_security"
  },
  "contributors": {
    "active_users": 156,
    "new_users_this_period": 23,
    "top_contributors": [
      {
        "user_id": "user_123abc",
        "username": "cyber_warrior",
        "contributions": 15,
        "points": 450
      }
    ]
  },
  "response_times": {
    "average_confirmation_time": "4 hours",
    "average_fix_time": "2 days",
    "fastest_fix": "30 minutes"
  }
}
```

---

#### `GET /analytics/threats/timeline`

Get threat timeline data for visualization.

**Response:** `200 OK`
```json
{
  "timeline": [
    {
      "date": "2025-01-01",
      "threats": 2,
      "critical": 0,
      "high": 1,
      "medium": 1,
      "low": 0
    },
    {
      "date": "2025-01-02",
      "threats": 3,
      "critical": 1,
      "high": 1,
      "medium": 1,
      "low": 0
    }
  ]
}
```

---

### Contributions Endpoints

#### `GET /contributions`

List user contributions.

**Query Parameters:**
- `user_id`: Filter by user
- `type`: Filter by contribution type (`threat_report`, `code_review`, `documentation`, `testing`)
- `status`: Filter by status

**Response:** `200 OK`
```json
{
  "contributions": [
    {
      "contribution_id": "contrib_123",
      "type": "threat_report",
      "user_id": "user_123abc",
      "username": "cyber_warrior",
      "content": {
        "threat_id": "THREAT-2025-001",
        "title": "SQL Injection in Auth Module"
      },
      "status": "accepted",
      "points_earned": 100,
      "created_at": "2025-01-10T10:00:00Z"
    }
  ],
  "pagination": { ... }
}
```

---

#### `GET /contributions/me`

Get current user's contributions.

**Response:** `200 OK`
```json
{
  "total_contributions": 42,
  "total_points": 1337,
  "rank": "Elite Defender",
  "contributions_by_type": {
    "threat_report": 25,
    "code_review": 10,
    "documentation": 5,
    "testing": 2
  },
  "recent_contributions": [ ... ],
  "badges_earned": [ ... ]
}
```

---

## 📊 Data Models

### User Model

```typescript
interface User {
  user_id: string;
  username: string;
  email: string;
  profile: {
    full_name?: string;
    avatar_url?: string;
    bio?: string;
    location?: string;
    website?: string;
  };
  stats: {
    contributions: number;
    points: number;
    rank: string;
    badges: Badge[];
  };
  role: 'guest' | 'contributor' | 'maintainer' | 'admin';
  created_at: string; // ISO 8601
  updated_at: string;
  last_login?: string;
}
```

### Threat Model

```typescript
interface Threat {
  threat_id: string;
  title: string;
  description: string;
  severity: 'low' | 'medium' | 'high' | 'critical';
  status: 'reported' | 'investigating' | 'confirmed' | 'fixed' | 'closed';
  category: string;
  tags: string[];
  technical_details?: {
    affected_component?: string;
    vulnerable_code?: string;
    exploit_scenario?: string;
    proof_of_concept?: string;
  };
  cvss?: {
    score: number;
    vector: string;
    severity: string;
  };
  discovered_by: {
    user_id: string;
    username: string;
  };
  timeline: TimelineEvent[];
  affected_versions?: string[];
  fixed_in_version?: string;
  references?: string[];
  created_at: string;
  updated_at: string;
}
```

### Report Model

```typescript
interface Report {
  report_id: string;
  type: 'vulnerability' | 'incident' | 'audit' | 'analysis';
  title: string;
  summary: {
    total_threats: number;
    critical: number;
    high: number;
    medium: number;
    low: number;
  };
  findings: Finding[];
  recommendations: string[];
  metrics?: object;
  format: 'pdf' | 'html' | 'json' | 'markdown';
  file_url?: string;
  generated_by: {
    user_id: string;
    automation: boolean;
  };
  published: boolean;
  created_at: string;
}
```

---

## ⚠️ Error Handling

### Error Response Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "severity",
        "message": "Invalid severity level. Must be one of: low, medium, high, critical"
      }
    ],
    "request_id": "req_abc123",
    "timestamp": "2025-01-15T10:30:00Z"
  }
}
```

### HTTP Status Codes

| Code | Meaning | Description |
|------|---------|-------------|
| `200` | OK | Request successful |
| `201` | Created | Resource created successfully |
| `202` | Accepted | Request accepted (async processing) |
| `204` | No Content | Success with no response body |
| `400` | Bad Request | Invalid request parameters |
| `401` | Unauthorized | Authentication required |
| `403` | Forbidden | Insufficient permissions |
| `404` | Not Found | Resource not found |
| `409` | Conflict | Resource already exists |
| `422` | Unprocessable Entity | Validation error |
| `429` | Too Many Requests | Rate limit exceeded |
| `500` | Internal Server Error | Server error |
| `503` | Service Unavailable | Service temporarily unavailable |

### Common Error Codes

```
AUTHENTICATION_REQUIRED    - Authentication token missing
INVALID_TOKEN             - Invalid or expired token
INSUFFICIENT_PERMISSIONS   - User lacks required permissions
VALIDATION_ERROR          - Request validation failed
RESOURCE_NOT_FOUND        - Requested resource not found
RATE_LIMIT_EXCEEDED       - Too many requests
INTERNAL_ERROR            - Internal server error
SERVICE_UNAVAILABLE       - Service temporarily down
```

### Error Handling Example

```python
import requests

try:
    response = requests.post(
        'https://api.genesislink.io/v1/threats',
        headers={'Authorization': f'Bearer {token}'},
        json=threat_data
    )
    response.raise_for_status()
    threat = response.json()
