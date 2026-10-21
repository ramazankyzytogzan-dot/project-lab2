# STRIDE Threat Model — CafeFlow

## Component Architecture Boundaries
`[ User Browser ] -> ( Trust Boundary ) -> [ Express API Backend ] -> ( Database Boundary ) -> [ PostgreSQL DB ]`

## STRIDE Threat Analysis

| Category | Threat Description | Mitigation Measure | Status |
| :--- | :--- | :--- | :---: |
| **S (Spoofing)** | JWT токенін ұрлап, өзін кассир ретінде көрсету. | JWT токенге HMAC қолтаңбасын қосу және өмір сүруін 15 минутқа шектеу. | Done |
| **T (Tampering)** | Төлем чегінің соммасын MitM шабуылымен өзгерту. | HTTPS/TLS 1.3 шифрлауын және API сұраныстарын HMAC-SHA256 хешпен тексеру. | In Progress |
| **R (Repudiation)** | Кассир тапсырысты өшіріп, танымауы. | Барлық критикалық әрекеттерді PostgreSQL `audit_logs` кестесіне жазу. | Done |
| **I (Information Disclosure)** | База бұзылғанда клиент нөмірлерінің ашық тарауы. | Деректерді AES-256 арқылы базада шифрлап сақтау. | To Do |
| **D (Denial of Service)** | API-ге 10 000 сұраныс жіберіп, KDS экранын қатыру. | `express-rate-limit` арқылы 1 IP-ге 100 сұраныс лимитін қою. | To Do |
| **E (Elevation of Privilege)** | Кассир рольімен админ панеліне кіру. | RBAC (Role-Based Access Control) middleware арқылы рольді тексеру. | Done |
