# Technical Writing Lab

**Name:** Duop yien
**Date:** 5 October 2026
**Course:** Software Engineering
**Learning Hub:** Girl Power

This repository contains the two documentation deliverables for the lab:

1. [Part A: User Manual Procedure](#part-a-user-manual-procedure): creating and activating a Python virtual environment and installing a package
2. [Part B: API Reference Entry](#part-b-api-reference-entry): `POST /projects/{project_id}/tasks` (create a task)

---

# Part A: User Manual Procedure

## Creating and Activating a Python Virtual Environment and Installing a Package

### Purpose

This procedure shows you how to create an isolated Python workspace (a *virtual environment*), switch it on, and install a package inside it. A virtual environment keeps each project's packages separate, so installing something for one project cannot break another.

### Prerequisites

Before you start, make sure you have:

- **A computer** running Windows 10/11, macOS, or Linux
- **Python 3.8 or newer** installed. If you are installing it now on Windows, tick **"Add python.exe to PATH"** on the first installer screen.
- **An internet connection**, needed to download the package in Step 9
- **A terminal program:**
  - Windows: PowerShell (search "PowerShell" in the Start menu)
  - macOS: Terminal (Applications > Utilities)
  - Linux: any terminal (usually preinstalled)
- **About 50 MB of free disk space**
- **Basic command-line skill:** you can type a command exactly as shown and press Enter

**How to read the commands:** Text in code blocks is typed into the terminal, then you press **Enter**. Windows (PowerShell) commands are shown first; the macOS/Linux version follows where it differs.

### Procedure

**Step 1. Open your terminal.**
Open PowerShell (Windows) or Terminal (macOS/Linux).
*Expected result:* A window opens with a blinking cursor after a line ending in `>` or `$`. This line is called the *prompt*.

**Step 2. Check that Python is installed.**

```
python --version
```

macOS/Linux:

```
python3 --version
```

*Expected result:* The terminal prints a version such as `Python 3.12.4`. Any version 3.8 or higher is fine.

**Step 3. Create a new folder for your project.**

```
mkdir my_project
```

*Expected result:* No error appears and a fresh prompt is shown.

**Step 4. Move into the new folder.**

```
cd my_project
```

*Expected result:* The prompt now ends with `my_project`.

**Step 5. Create the virtual environment.**

```
python -m venv .venv
```

macOS/Linux:

```
python3 -m venv .venv
```

*Expected result:* After a few seconds the prompt returns with no error message.

**Step 6. Confirm that the environment folder exists.**

```
dir
```

macOS/Linux:

```
ls -a
```

*Expected result:* The listing includes a folder named `.venv`.

**Step 7. Activate the virtual environment.**

```
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```
source .venv/bin/activate
```

*Expected result:* The command prints nothing, but the prompt changes (see Step 8).

**Step 8. Check that activation worked.**
Look at the start of your prompt line.
*Expected result:* The text `(.venv)` appears at the very beginning of the prompt.

> **Screenshot 1 (place after Step 8)**
> **What it shows:** A cropped PowerShell window with a dark background and a light-coloured prompt. The last line reads `(.venv) PS C:\Users\student\my_project>`. A red rectangle surrounds `(.venv)`, with a callout arrow labelled "Activation indicator: this means the environment is activated." The lines above show the commands from Steps 3, 5 and 6 so the reader can see the sequence they followed.

**Step 9. Install a package called `requests`.**

```
pip install requests
```

*Expected result:* Several lines scroll by, ending with `Successfully installed requests-2.x.x` plus a few supporting packages.

**Step 10. List the installed packages.**

```
pip list
```

*Expected result:* A table appears that includes `requests`, `pip` and several helper packages.

**Step 11. Test that Python can use the package.**

```
python -c "import requests; print(requests.__version__)"
```

*Expected result:* A version number such as `2.32.3` is printed with no error.

> **Screenshot 2 (place after Step 11)**
> **What it shows:** A terminal window showing the output of Steps 9 to 11: the `Successfully installed requests-2.x.x` line, the `pip list` table with the `requests` row highlighted in yellow, and the printed version number at the bottom. The caption underneath reads: "These three outputs confirm that the package was installed inside the virtual environment."

**Step 12. Deactivate the environment when you are finished.**

```
deactivate
```

*Expected result:* The `(.venv)` prefix disappears from the prompt.

### Troubleshooting: "running scripts is disabled on this system" (Windows)

**What you see in Step 7:** A red error message saying `Activate.ps1 cannot be loaded because running scripts is disabled on this system`.

**Why it happens:** Windows PowerShell blocks scripts by default for security, and the activation file is a PowerShell script.

**How to fix it:**

1. In the same PowerShell window, type:
   ```
   Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
   ```
2. When asked to confirm, type `Y` and press Enter.
3. Run the activation command from Step 7 again.

*Expected result:* `(.venv)` appears at the start of the prompt. The change applies only to your user account and persists for future sessions.

**Alternative:** If you prefer not to change this setting, open **Command Prompt** instead and use `.venv\Scripts\activate.bat` in Step 7.

### Quick Reference

| Goal | Command |
|---|---|
| Create environment | `python -m venv .venv` |
| Activate (Windows) | `.venv\Scripts\Activate.ps1` |
| Activate (macOS/Linux) | `source .venv/bin/activate` |
| Install a package | `pip install <package-name>` |
| Deactivate | `deactivate` |

---

# Part B: API Reference Entry

The application documented here is a fictional project management service called **TaskFlow**. This entry documents the endpoint that creates a task inside a project.

## Create a Task

Creates a new task in the specified project and returns the created task.

```
POST https://api.taskflow.example.com/v1/projects/{project_id}/tasks
```

### Authentication

Every request must include a valid API token in the `Authorization` header. Tokens are created in **Account Settings > API Tokens**. The token's owner must be a member of the project with the *Editor* or *Admin* role.

### Request Headers

| Header | Required | Value | Description |
|---|---|---|---|
| `Authorization` | Yes | `Bearer <API_TOKEN>` | Identifies and authenticates the caller. |
| `Content-Type` | Yes | `application/json` | Format of the request body. |
| `Accept` | No | `application/json` | Format of the response. JSON is the default. |

### Path Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `project_id` | string | Yes | Unique ID of the project that will contain the task, for example `prj_8f3a21`. |

### Request Body Parameters

| Field | Type | Required | Default | Constraints | Description |
|---|---|---|---|---|---|
| `title` | string | Yes | none | 1 to 200 characters | Short name of the task. |
| `description` | string | No | `""` | Up to 2,000 characters | Detailed explanation of the work. |
| `assignee_id` | string | No | `null` | Must be an existing project member ID | The user responsible for the task. |
| `due_date` | string | No | `null` | ISO 8601 date (`YYYY-MM-DD`), not in the past | Date the task is due. |
| `priority` | string | No | `"medium"` | One of `low`, `medium`, `high`, `urgent` | Importance of the task. |
| `status` | string | No | `"todo"` | One of `todo`, `in_progress`, `done` | Initial workflow state. |
| `labels` | array of strings | No | `[]` | Up to 10 items, each up to 30 characters | Tags used to group and filter tasks. |

### Example Request

```bash
curl -X POST "https://api.taskflow.example.com/v1/projects/prj_8f3a21/tasks" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Design login page",
    "description": "Create wireframes for the login and sign-up screens.",
    "assignee_id": "usr_41c7de",
    "due_date": "2026-10-20",
    "priority": "high",
    "labels": ["design", "frontend"]
  }'
```

### Example Success Response

**Status:** `201 Created`
The `Location` response header contains the URL of the new task.

```json
{
  "id": "tsk_5d92b0",
  "project_id": "prj_8f3a21",
  "title": "Design login page",
  "description": "Create wireframes for the login and sign-up screens.",
  "assignee_id": "usr_41c7de",
  "due_date": "2026-10-20",
  "priority": "high",
  "status": "todo",
  "labels": ["design", "frontend"],
  "created_by": "usr_29ab10",
  "created_at": "2026-10-05T09:30:00Z",
  "updated_at": "2026-10-05T09:30:00Z"
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique ID generated for the task. |
| `project_id` | string | ID of the project that contains the task. |
| `title` | string | Task title as submitted. |
| `description` | string | Task description (empty string if none was given). |
| `assignee_id` | string or null | ID of the assigned user, or `null`. |
| `due_date` | string or null | Due date in `YYYY-MM-DD` format, or `null`. |
| `priority` | string | `low`, `medium`, `high` or `urgent`. |
| `status` | string | `todo`, `in_progress` or `done`. |
| `labels` | array of strings | Tags attached to the task. |
| `created_by` | string | ID of the user who owns the API token used. |
| `created_at` | string | Creation time in ISO 8601 UTC format. |
| `updated_at` | string | Time of the last change, in ISO 8601 UTC format. |

### Status Codes

| Code | Meaning | When it occurs |
|---|---|---|
| `201 Created` | Success | The task was created. |
| `400 Bad Request` | Malformed request | The body is not valid JSON. |
| `401 Unauthorized` | Authentication failed | The `Authorization` header is missing, malformed, or the token is invalid or expired. |
| `403 Forbidden` | Not permitted | The token owner is not an Editor or Admin of the project. |
| `404 Not Found` | Resource missing | The `project_id` does not exist, or `assignee_id` is not a project member. |
| `422 Unprocessable Entity` | Validation failed | A required field is missing or a value breaks a constraint (for example, an empty `title` or an invalid `priority`). |
| `429 Too Many Requests` | Rate limit exceeded | More than 100 requests per minute from one token. Retry after the number of seconds in the `Retry-After` header. |
| `500 Internal Server Error` | Server problem | An unexpected error occurred. Retry later; contact support if it persists. |

### Example Error Response

**Status:** `422 Unprocessable Entity`

```json
{
  "error": {
    "code": "validation_failed",
    "message": "The request body contains invalid fields.",
    "details": [
      { "field": "title", "issue": "This field is required." },
      { "field": "priority", "issue": "Must be one of: low, medium, high, urgent." }
    ]
  }
}
```

**Status:** `401 Unauthorized`

```json
{
  "error": {
    "code": "invalid_token",
    "message": "The API token is missing, invalid, or expired."
  }
}
```
