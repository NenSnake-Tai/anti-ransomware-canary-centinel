# Anti-Ransomware Canary Centinel 🛡️

A low-latency behavioral anti-ransomware suite built in Node.js. This repository provides dual-environment implementation architecture to monitor file system structures and enforce immediate process mitigation upon unauthorized cryptographic alterations.

## 🗂️ Environment Architecture (How to run the scripts)

The suite is divided into two operational environments depending on your target hardware deployment:

### 🟢 1. Production Environment (Real PC / Server)
* **File:** `canario-prod.js`
* **Target Hardware:** Desktop Computers, Laptops, and Enterprise Servers running Windows, Linux, or macOS with active local storage access.
* **Operational Flow:** Deploys physical honeypot directories directly into the file system. It leverages native Node.js core modules (`fs`) to monitor hardware storage in cold isolation.
* **Execution Command:**
  ```bash
  node canario-prod.js
  ```

### 📱 2. Live Simulation Environment (Mobile App / Virtual Engine)
* **File:** `canario.js`
* **Target Hardware:** Mobile devices, tablets, and sandboxed in-app console environments (such as Acode internal engines).
* **Operational Flow:** Virtualizes the behavioral detection loop strictly inside the volatile RAM buffer via global runtime engines (`globalThis`), avoiding environment crashes or file system sandbox restrictions.
* **Execution Flow:** Run the script in your in-app console. To simulate an active ransomware infection vector, execute:
  ```javascript
  simularAtaqueRansomware()
  ```

---
*Disclaimer: Developed for behavioral defense assessment and advanced threat analysis.*


```mermaid
graph TD
    %% Estilo de nodos neón
    classDef safe color:#00ff66,fill:#000,stroke:#00ff66,stroke-width:2px;
    classDef alert color:#ff0033,fill:#000,stroke:#ff0033,stroke-width:2px;
    classDef process color:#00ffff,fill:#000,stroke:#00ffff,stroke-width:1px;

    Start([⚡ Arranque del Sistema]) --> Deploy[🚀 Despliegue de Carpeta Cebo .honeypot-trap]
    Deploy --> Write[📝 Inyección de Firma Frecuencial canario.txt]
    Write --> Listen[📡 Escucha Pasiva del Kernel a 120Hz fs.watch]
    
    Listen --> Check{👾 ¿Intento de Intrusión / Evento Detectado?}
    
    Check -- NO --> Listen
    Check -- SÍ --> Verify[🔬 Auditoría Rápida de Bytes en RAM/Disco]
    
    Verify --> Logic{⚠️ ¿Firma alterada o archivo eliminado?}
    
    Logic -- NO --> Listen
    
    Logic -- SÍ --> Alert[🚨 ALERTA CRÍTICA DETECTADA]:::alert
    Alert --> Freeze[🔒 INSTANT SYSTEM FREEZE process.exit]:::alert
    Freeze --> End([🛑 Aislamiento de Disco a Cero Lag]):::alert

    class Start,Deploy,Write,Listen safe;
    class Check,Verify,Logic process;
```
