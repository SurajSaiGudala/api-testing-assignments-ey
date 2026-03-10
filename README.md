 API Test Template — Postman
 
 Files:
 - postman-collection-template.json — Postman collection (v2.1.0) with generated tests. Now includes:
	 - `Create Post (example)` — POST request with assertions and stores `createdId` in environment.
	 - `Get Created Post` — GET using `{{createdId}}` and assertions verifying the created resource.
	 - `Get Posts` — list request with stronger schema/type checks and header assertions.
 
 Quick usage:
 1) Open Postman.
 2) Import > File > choose postman-collection-template.json.
 3) Edit the `baseUrl` collection variable to point to your API.
 4) Run individual requests or use the Collection Runner to execute tests.
 
 Notes:
 - This template uses basic PM test assertions (pm.test, pm.response, pm.expect).
 - Customize request bodies, headers, and additional assertions as needed.
 
 Advanced: to run with Newman (no Postman UI):
 ```
 npx newman run postman-template/postman-collection-template.json --insecure
 ```
 Use `--insecure` only for debugging when facing TLS/CA issues; prefer adding your CA via `NODE_EXTRA_CA_CERTS`.
 
Configuration:
- **maxResponseTime**: collection variable that sets the acceptable response time (in ms) for assertions that check latency. Default: `5000`.
	- To change the threshold in Postman: open the collection, edit the `maxResponseTime` variable.
	- To override for Newman runs, set an environment variable or edit the exported collection before running.
 
Environment file:
- An environment file `postman-environment.json` is included in this folder to make it easy to override variables for Newman runs. It contains `baseUrl` and `maxResponseTime` (default `2000`).
- Run with the environment:
```
npx newman run postman-template/postman-collection-template.json --environment postman-template/postman-environment.json --insecure
```
You can edit `postman-environment.json` to change `maxResponseTime` prior to running, or export a Postman environment and pass it to Newman.

Notes:
- This template uses basic PM test assertions (pm.test, pm.response, pm.expect).
- Customize request bodies, headers, and additional assertions as needed.

Want me to generate tests for a specific API (provide base URL and endpoints)?
