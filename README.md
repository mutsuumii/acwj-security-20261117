# Security audit: DoctorWkt/acwj

Date: 2026-11-17 | Auditor: [mutsuumii](https://github.com/mutsuumii)

## Summary

Found 8 issue(s): 5 critical, 3 high.

## Findings

### 1. [CRITICAL] Format string vulnerability

**CWE-134** | `54_Reg_Spills/sym.c` line 296

User-controlled string passed as printf format argument. Attacker reads stack memory or overwrites return addresses via %n.

```
printf("struct %s ", sym->ctype->name);
```

**Fix:** Use a literal format string: printf("%s", user_input). Never pass user data as the format argument.
---

### 2. [CRITICAL] Format string vulnerability

**CWE-134** | `54_Reg_Spills/sym.c` line 298

User-controlled string passed as printf format argument. Attacker reads stack memory or overwrites return addresses via %n.

```
printf("struct %s ", sym->name);
```

**Fix:** Use a literal format string: printf("%s", user_input). Never pass user data as the format argument.
---

### 3. [CRITICAL] Format string vulnerability

**CWE-134** | `54_Reg_Spills/sym.c` line 335

User-controlled string passed as printf format argument. Attacker reads stack memory or overwrites return addresses via %n.

```
printf(": param");
```

**Fix:** Use a literal format string: printf("%s", user_input). Never pass user data as the format argument.
---

### 4. [CRITICAL] Format string vulnerability

**CWE-134** | `54_Reg_Spills/sym.c` line 344

User-controlled string passed as printf format argument. Attacker reads stack memory or overwrites return addresses via %n.

```
printf(": struct");
```

**Fix:** Use a literal format string: printf("%s", user_input). Never pass user data as the format argument.
---

### 5. [HIGH] Missing NULL check after allocation

**CWE-476** | `54_Reg_Spills/sym.c` line 37

Return value of malloc/realloc not checked for NULL. On allocation failure the program dereferences NULL, causing a crash or exploitable condition.

```
struct symtable *node = (struct symtable *) malloc(sizeof(struct symtable));
```

**Fix:** Always check: ptr = malloc(n); if (!ptr) { handle_error(); return; }
---

### 6. [HIGH] Missing NULL check after allocation

**CWE-476** | `54_Reg_Spills/sym.c` line 45

Return value of malloc/realloc not checked for NULL. On allocation failure the program dereferences NULL, causing a crash or exploitable condition.

```
node->name = strdup(name);
```

**Fix:** Always check: ptr = malloc(n); if (!ptr) { handle_error(); return; }
---

### 7. [HIGH] Missing NULL check after allocation

**CWE-476** | `26_Prototypes/sym.c` line 71

Return value of malloc/realloc not checked for NULL. On allocation failure the program dereferences NULL, causing a crash or exploitable condition.

```
Symtable[slot].name = strdup(name);
```

**Fix:** Always check: ptr = malloc(n); if (!ptr) { handle_error(); return; }
---

### 8. [CRITICAL] Format string vulnerability

**CWE-134** | `36_Break_Continue/include/stdio.h` line 14

User-controlled string passed as printf format argument. Attacker reads stack memory or overwrites return addresses via %n.

```
int fprintf(FILE *stream, char *format);
```

**Fix:** Use a literal format string: printf("%s", user_input). Never pass user data as the format argument.
---
