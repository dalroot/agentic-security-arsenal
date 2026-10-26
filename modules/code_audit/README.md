# Code Audit Module (White-box Security)

This module provides rules, automated SAST commands, and checklists for auditing PHP, WordPress plugins/themes, and web application source code.

---

## 1. Quick Start with Semgrep

Install Semgrep (if not already installed):
```bash
pip install semgrep
```

Run custom WordPress security rules against a target repository:
```bash
semgrep --config ./modules/code_audit/rules/semgrep_wordpress.yml <path_to_plugin> --json -o semgrep_results.json
```

Or run the full official community security ruleset:
```bash
semgrep --config "p/php" --config "p/owasp-top-ten" <path_to_plugin> --json
```

---

## 2. Key Audit Vectors in WordPress / PHP

### A. Authentication & Permission Bypass (REST API)
- Look for `register_rest_route` where:
  - `'permission_callback' => '__return_true'`
  - Or `'permission_callback' => null` (WordPress deprecated, but still prevalent in legacy code).
- Even if a custom token/nonce is verified (e.g. `check_custom_nonce`), verify if the token is stored in predictable storage, has race conditions, or if brute-force is feasible.

### B. Missing Capability & Nonce Verification
- Every state-changing action (`delete`, `update`, `approve`) must check:
  1. **User Identity & Role:** `current_user_can('edit_post', $post_id)` or `current_user_can('manage_options')`.
  2. **CSRF Protection:** `wp_verify_nonce($_REQUEST['_wpnonce'], 'action_name')` or `check_admin_referer()`.
- **Trap:** Checking the nonce alone does NOT prevent horizontal privilege escalation if any logged-in subscriber can generate a valid user nonce!

### C. Unauthenticated AJAX Handlers
- Grep for `wp_ajax_nopriv_`:
```bash
grep -rn "wp_ajax_nopriv_" <path_to_plugin>
```
- Verify whether the attached callback function exposes sensitive operations or information to anonymous visitors.
