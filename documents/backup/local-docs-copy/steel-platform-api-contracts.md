# Steel Platform API Contracts

## 1. Purpose

This document defines proposed interfaces for the first implementation.

These contracts are intended to give an AI coding agent a clear target for service interfaces.

## 2. Service Endpoints

### 2.1 Control Gateway

Base path:

- `/api/v1`

Recommended endpoints:

- `POST /sessions`
- `GET /sessions/{session_id}`
- `POST /actions/open`
- `POST /actions/click`
- `POST /actions/type`
- `POST /actions/wait`
- `POST /actions/extract`
- `POST /actions/screenshot`

### 2.2 Content Normalizer

Base path:

- `/normalize/v1`

Recommended endpoints:

- `POST /page`
- `POST /html`

## 3. Shared Response Envelope

All control-layer responses should use a common shape.

```json
{
  "ok": true,
  "request_id": "req_123",
  "session_id": "sess_123",
  "result": {},
  "error": null
}
```

## 4. Session Endpoints

### POST /sessions

Purpose:

- create a reusable browser session

Request:

```json
{
  "profile": "default",
  "metadata": {
    "site": "example.com"
  }
}
```

Response:

```json
{
  "ok": true,
  "request_id": "req_1",
  "session_id": "sess_1",
  "result": {
    "session_id": "sess_1",
    "status": "created"
  },
  "error": null
}
```

## 5. Action Endpoints

### POST /actions/open

Request:

```json
{
  "session_id": "sess_1",
  "url": "https://example.com"
}
```

### POST /actions/click

Request:

```json
{
  "session_id": "sess_1",
  "target": {
    "selector_hint": "button.login",
    "text": "Login",
    "id": "btn_1"
  }
}
```

### POST /actions/type

Request:

```json
{
  "session_id": "sess_1",
  "target": {
    "selector_hint": "input[type=email]",
    "id": "inp_1"
  },
  "text": "user@example.com"
}
```

### POST /actions/wait

Request:

```json
{
  "session_id": "sess_1",
  "condition": {
    "selector_hint": ".dashboard",
    "timeout_ms": 10000
  }
}
```

### POST /actions/extract

Purpose:

- fetch current browser state and run normalization

Request:

```json
{
  "session_id": "sess_1",
  "mode": "full"
}
```

Response:

```json
{
  "ok": true,
  "request_id": "req_9",
  "session_id": "sess_1",
  "result": {
    "page_meta": {
      "url": "https://example.com",
      "title": "Example"
    },
    "semantic_summary": {
      "page_type": "landing_page",
      "main_content_markdown": "# Example\n\nMain content",
      "important_sections": ["Hero", "Pricing"]
    },
    "actionable_view": {
      "buttons": [],
      "links": [],
      "inputs": [],
      "forms": []
    },
    "artifacts": {
      "raw_html_ref": "artifact://page/1/raw-html",
      "screenshot_ref": "artifact://page/1/screenshot"
    }
  },
  "error": null
}
```

### POST /actions/screenshot

Request:

```json
{
  "session_id": "sess_1"
}
```

## 6. Normalizer Contract

### POST /normalize/v1/page

Request:

```json
{
  "page_meta": {
    "url": "https://example.com",
    "title": "Example"
  },
  "raw_html": "<html>...</html>",
  "visible_text": "Visible text here",
  "elements": {
    "links": [],
    "buttons": [],
    "inputs": [],
    "forms": []
  },
  "artifacts": {
    "screenshot_ref": "artifact://page/1/screenshot"
  }
}
```

Response:

```json
{
  "page_meta": {
    "url": "https://example.com",
    "title": "Example"
  },
  "semantic_summary": {
    "page_type": "article",
    "main_content_markdown": "# Example\n\nSummary",
    "important_sections": ["Section 1"]
  },
  "actionable_view": {
    "links": [],
    "buttons": [],
    "inputs": [],
    "forms": []
  },
  "artifacts": {
    "raw_html_ref": "artifact://page/1/raw-html",
    "screenshot_ref": "artifact://page/1/screenshot"
  },
  "metrics": {
    "raw_html_chars": 85000,
    "normalized_chars": 6200
  }
}
```

## 7. Error Shape

```json
{
  "ok": false,
  "request_id": "req_404",
  "session_id": "sess_1",
  "result": null,
  "error": {
    "code": "ACTION_FAILED",
    "message": "Click target not found",
    "details": {
      "target_id": "btn_1"
    }
  }
}
```

## 8. Contract Rules

- browser actions should not return raw HTML by default
- extraction actions should pass through normalization by default
- action endpoints should always accept `session_id`
- actionable data should preserve stable IDs where possible
- every response should carry `request_id`

