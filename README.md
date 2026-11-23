## Reflections

1. **Why separate Vue and Express?** Keeping everything in Vue felt simpler when the board only read a static file. With Express, the server has one place to define the animal data and decide what each request returns. Vue can focus on displaying those results and responding to button clicks. If I add a database later, I can change how the server gets the data while keeping the same API for Vue.
2. **How could I use this setup in my final project?** In my diabetes prediction project, the client could display the input form, the prediction, and the what-if results. The server could validate the submitted values, run the model, and send the results back as JSON. A user could adjust an input on the page and see the new result without needing to run the model on their own device.
3. **Vue or vanilla JavaScript?** I prefer Vue for a board like this because the list and available count update when the animal data changes. I can keep the controls and cards in separate components and use a computed property for the visible list. For a simple page with one button and one event, I would still consider vanilla JavaScript.

# Assignment 6 — Adding the Server

The animal adoption board loads eight animals from an in-memory Express API. Vue displays the animals and handles sorting, filtering, and temporary adoption changes. Adopt and Return update the browser's copy, so refreshing reloads the server's original data.

## Run locally

Use Node.js 22.12 or later. Install dependencies from the project folder.

```bash
npm ci
```

Start Express in one terminal.

```bash
node --watch server.js
```

Start Vue in a second terminal.

```bash
npm run dev
```

Open the local URL printed by Vite. Vite forwards requests under `/api` to Express on port 3000.

## API routes

| GET request | Status | JSON response |
| --- | --- | --- |
| `/api/animals` | 200 | All animals |
| `/api/animals/available` | 200 | Available animals |
| `/api/animals/adopted` | 200 | Adopted animals |
| `/api/animals/3` | 200 | Pepper's record |
| `/api/animals/999` | 404 | `{"error":"Animal not found"}` |

The filtered lists are also available at `/api/available-animals` and `/api/adopted-animals`. The fixed filter routes are registered before `/api/animals/:id` so their names reach the correct handlers.
