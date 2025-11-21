# Backend API Endpoints Reference

## Complete List of Available Endpoints

### Authentication & User Management
**Base Path:** `/api/v1/users`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/users/register` | POST | Register new user | No |
| `/api/v1/users/me/:authProviderId` | GET | Get user by Firebase ID | No |
| `/api/v1/users/me` | DELETE | Delete user account | Yes |
| `/api/v1/users/me/export` | GET | Export all user data | Yes |

**Note:** `DELETE /api/v1/users/me` and `GET /api/v1/users/me/export` require authentication (Authorization header)

---

### Subscription Management
**Base Path:** `/api/v1/subscription`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/subscription/me` | GET | Get current user's subscription | Yes |
| `/api/v1/subscription/me` | PUT | Update current user's subscription tier | Yes |

**GET Response:**
```json
{
  "success": true,
  "data": {
    "tier": "premium",
    "isActive": true,
    "expiresAt": null,
    "features": ["basic_questions", "portfolio_view", "ai_chat", "recommendations"],
    "limits": {
      "aiRequestsPer15min": 2,
      "aiRequestsPerDay": 20,
      "standardRequestsPer15min": 100,
      "publicRequestsPer15min": 200
    }
  }
}
```

**PUT Request:**
```json
{
  "tier": "premium",
  "billingPeriod": "monthly"
}
```

**PUT Response:** Same format as GET response (returns updated subscription)

**See:** `docs/guides/api/subscription-update-endpoint.md` for detailed integration guide

---

### Session Management
**Base Path:** `/api/v1/sessions`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/sessions/refresh` | POST | Refresh session token | Yes |
| `/api/v1/sessions/status` | GET | Get session status | Yes |
| `/api/v1/sessions/logout` | POST | Logout (invalidate session) | Yes |
| `/api/v1/sessions/logout-all` | POST | Logout all devices | Yes |

---

### User Responses & Assessment
**Base Path:** `/api/v1/user-responses`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/user-responses/session` | POST | Create new session | No |
| `/api/v1/user-responses/user/:firebaseId/sessions` | GET | Get all sessions for user | No |
| `/api/v1/user-responses/session/:id` | GET | Get session by ID | No |
| `/api/v1/user-responses/answer` | POST | Save answer | No |
| `/api/v1/user-responses/answers/bulk` | POST | Save multiple answers | No |
| `/api/v1/user-responses/session/:id/questions-answers` | GET | Get Q&A for session | No |
| `/api/v1/user-responses/session/:id/resume` | GET | Get resume info | No |
| `/api/v1/user-responses/session/:id/complete` | POST | Mark session complete | No |

---

### Assessment Results
**Base Path:** `/api/v1/assessment`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/assessment/response-group/:id/answers` | GET | Get answered questions | No |
| `/api/v1/assessment/response-group/:id/category/:categoryName/answers` | GET | Get category answers | No |
| `/api/v1/assessment/response-group/:id/score` | GET | Get assessment score | No |
| `/api/v1/assessment/user/:firebaseId/latest` | GET | Get latest results | No |
| `/api/v1/assessment/user/:firebaseId/all` | GET | Get all results | No |

---

### Chat
**Base Path:** `/api/v1/chat`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/chat/:userId/send` | POST | Send AI chat message | Yes |
| `/api/v1/chat/:userId/messages` | GET | Get chat messages | Yes |
| `/api/v1/chat/:userId/conversation` | GET | Get conversation | Yes |
| `/api/v1/chat/:userId/debug-response-group` | GET | Debug endpoint | Yes |
| `/api/v1/chat/health/behavioral-analysis` | GET | Health check | No |

---

### Recommendations
**Base Path:** `/api/v1/recommendation`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/recommendation/response-group/:id` | GET | Get recommendations | No |

---

### Quiz
**Base Path:** `/api/v1/quiz`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/quiz/:assetClass` | GET | Get quiz questions | No |
| `/api/v1/quiz/validate` | POST | Validate answer | No |
| `/api/v1/quiz/submit` | POST | Submit quiz | No |
| `/api/v1/quiz/progress` | GET | Get quiz progress | No |

---

### Spending Analysis
**Base Path:** `/api/v1/spending`

All endpoints use query parameter `?userId={firebaseId}`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/spending/overview` | POST | Save spending overview | No |
| `/api/v1/spending/overview` | GET | Get spending overview | No |
| `/api/v1/spending/categories` | POST | Add category | No |
| `/api/v1/spending/categories` | GET | Get categories | No |
| `/api/v1/spending/recommendations` | GET | Get recommendations | No |
| `/api/v1/spending/cash-flow-projections` | GET | Get projections | No |


### Goals Management
**Base Path:** `/api/v1/goals`

All endpoints use query parameter `?userId={firebaseId}`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/api/v1/goals` | POST | Create a new financial goal | No |
| `/api/v1/goals` | GET | Get all goals for a user | No |
| `/api/v1/goals/:goalId` | GET | Get a specific goal by ID | No |
| `/api/v1/goals/:goalId` | PUT | Update a goal | No |
| `/api/v1/goals/:goalId` | DELETE | Delete a goal | No |
| `/api/v1/goals/:goalId/progress` | GET | Get goal progress history | No |
| `/api/v1/goals/simulate-strategy` | POST | Simulate goal allocation strategy with custom budget | No |

**POST /api/v1/goals Request Body:**
```json
{
  "goalName": "Retirement",
  "goalType": "retirement",
  "targetAmount": 1000000,
  "currentAmount": 0,
  "monthlyContribution": 1000,
  "investmentHorizon": 20,
  "targetYear": 2045,
  "priority": 1,
  "riskLevel": "medium"
}
```

**GET /api/v1/goals Response:**
```json
{
  "data": {
    "goals": [
      {
        "id": "uuid",
        "goalName": "Retirement",
        "goalType": "retirement",
        "targetAmount": "1000000.00",
        "currentAmount": "50000.00",
        "monthlyContribution": "1000.00",
        "investmentHorizon": 20,
        "progressPercentage": 5.0,
        "state": "on_track"
      }
    ],
    "summary": {
      "totalGoals": 3,
      "activeGoals": 2,
      "totalTargetAmount": "1500000.00"
    }
  }
}
```
---

### Health & Status
**Base Path:** `/health`

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/health` | GET | System health | No |
| `/health/db` | GET | Database health | No |


**For User Profile:**
```typescript
// Get user by Firebase UID (not database ID)
GET /api/v1/users/me/{firebaseUid}

// Example:
GET /api/v1/users/me/kpECLiIGUOg1dvRFgp7q3KzktL32
```

**For Learning Progress:**
```typescript
// Get latest assessment results
GET /api/v1/assessment/user/{firebaseUid}/latest

// Get all assessment results
GET /api/v1/assessment/user/{firebaseUid}/all

// Get quiz progress
GET /api/v1/quiz/progress?userId={firebaseUid}&assetClass={assetClass}
```

---

## Authentication

### Required Headers
```typescript
headers: {
  'Authorization': `Bearer ${firebaseToken}`,
  'Content-Type': 'application/json'
}
```

### Endpoints Requiring Auth:
- `/api/v1/users/me` (DELETE)
- `/api/v1/users/me/export` (GET)
- `/api/v1/subscription/me` (GET)
- `/api/v1/sessions/*` (all)
- `/api/v1/chat/:userId/*` (all)

**All others:** No auth required

---



