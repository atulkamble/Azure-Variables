# ✅ **1. Define Variables in Release Pipeline (Classic Editor)**

### **Steps (Classic Release Pipeline)**

1. Go to **Pipelines → Releases**
2. Edit your Release pipeline
3. Click **Variables** (top menu)
4. Add:

   * **Name:** `environment`
   * **Value:** `production`
   * Scope: **Release / Stage**

### **Use Variable in Script (Classic Release Task)**

```bash
echo "Deploying to $(environment)"
```

---

# ✅ **2. Create Variable Group (Library → Variable Groups)**

### Steps:

1. Go to **Pipelines → Library → + Variable Group**
2. Name: **my-var-group**
3. Add variables:

   * `appUrl = https://myapp.com`
   * `connectionString = Server=db;User=atul;Pwd=Ethans@123`
4. Enable **Allow access to all pipelines**

---

# 📌 **Use Variable Group in Build/Release Classic Editor**

### **Classic Pipeline → Variables → Link Variable Group**

* Click **Variable Groups**
* Select **my-var-group**

### **Use in Tasks**

```bash
echo "App URL: $(appUrl)"
echo "DB: $(connectionString)"
```

---

# ✅ **3. Use Variable Groups in YAML Pipeline**

### **Link Variable Group**

```yaml
variables:
- group: my-var-group
```

### **Use Variables from Group**

```yaml
steps:
- script: |
    echo "App URL = $(appUrl)"
    echo "ConnString = $(connectionString)"
  displayName: "Print Variables"
```

---

# 🎯 **4. Define Variables in YAML**

## (A) **Define Simple Variables**

```yaml
variables:
  appName: cloudnautic-app
  environment: dev
```

---

## (B) **Runtime Variables**

```yaml
variables:
  buildVersion: $[counter('ver', 1)]
```

---

## (C) **Set Variables in Script**

```yaml
steps:
- bash: |
    echo "##vso[task.setvariable variable=imageTag]v1.0.$(Build.BuildId)"
```

Use it later:

```yaml
- script: |
    echo "Image Tag: $(imageTag)"
```

---

# 🎯 **5. Ways to Refer Variables in Azure DevOps**

Azure DevOps supports **three referencing formats**:

---

## **1️⃣ Macro Expression — `$(variable)`**

Used at **runtime** (classic build, YAML, scripts).

✔️ Example:

```yaml
echo $(environment)
```

---

## **2️⃣ Template Expression — `${{ variables.varName }}`**

Used when variables must be resolved **at compile time** (before pipeline runs).

✔️ Example:

```yaml
variables:
  stageName: dev

stages:
- stage: ${{ variables.stageName }}
  jobs:
  - job: BuildJob
```

---

## **3️⃣ Runtime Expression — `$[ variables.varName ]`**

Used to evaluate at **runtime conditionally**.

✔️ Example:

```yaml
steps:
- script: echo $[ variables['appName'] ]
```

✔️ Conditional Runtime Expression:

```yaml
variables:
  env: 'prod'

steps:
- script: echo "Running for PROD"
  condition: eq(variables['env'], 'prod')
```

---

# 🔥 **6. Full Working YAML Pipeline – END-TO-END Example**

```yaml
trigger:
- main

variables:
  appName: cloudnautic-app
  environment: dev
  buildCounter: $[counter('buildVersion', 1)]

  # Variable Group
- group: my-var-group

stages:

- stage: Build
  displayName: "Build Stage"
  jobs:
  - job: BuildJob
    steps:

    - script: echo "Macro variable: $(appName)"
      displayName: "Macro Example"

    - script: echo "Template variable: ${{ variables.environment }}"
      displayName: "Template Example"

    - script: echo "Runtime variable: $[ variables.buildCounter ]"
      displayName: "Runtime Example"

    - script: |
        echo "Using variable from variable group:"
        echo "App URL: $(appUrl)"
      displayName: "Var Group Example"

    - bash: |
        echo "##vso[task.setvariable variable=imageTag]$(Build.BuildId)"
      displayName: "Set Variable from Script"

    - script: echo "Image Tag is: $(imageTag)"
      displayName: "Use Set Variable"
```

---

# 🎉 **7. Quick Reference Table**

| Type         | Syntax                 | Resolves When             | Example                             |
| ------------ | ---------------------- | ------------------------- | ----------------------------------- |
| **Macro**    | `$(var)`               | Runtime                   | `echo $(buildNumber)`               |
| **Template** | `${{ variables.var }}` | Compile time              | `stage: ${{ variables.stageName }}` |
| **Runtime**  | `$[ variables.var ]`   | Runtime (with conditions) | `$[ variables['appName'] ]`         |

---

