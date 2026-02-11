---

---
FastCGI is an implementation of the [[Common Gateway Interface]] protocol.
It exists because **forking per request is expensive**. Instead, a pool of [[Process]]es is constantly ready to process requests as they arrive.