# C1 App Template

Template repository for a generative UI app, powered by [C1 by Thesys](https://thesys.dev), and bootstrapped with `create-next-app`.

[![Built with Thesys](https://thesys.dev/built-with-thesys-badge.svg)](https://thesys.dev)

## Getting Started

First, generate a new API key from [Thesys Console](https://chat.thesys.dev/console/keys) and then set it as your environment variable.

```bash
export THESYS_API_KEY=<your-api-key>
```

Install dependencies:

```bash
npm i
```

Then, run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing your responses by modifying the system prompt in `src/app/api/chat/route.ts`.

---

## Custom Chat UI with Dark Mode

This template now includes a **customizable chat UI** with support for dark mode. The UI is built with React and Tailwind CSS, and includes the following components:

### File Structure

```
src/
  components/
    ChatMessage.tsx   # Individual message bubbles
    ChatInput.tsx     # Input field and send button
    ChatWindow.tsx    # Container for all messages
    ThemeToggle.tsx   # Toggle for dark/light mode
  app/
    page.tsx          # Main page rendering the chat
    globals.css       # Global styles and dark mode variables
```

### Features

- **ChatMessage**: Customizable message bubbles for user and AI, with timestamps.
- **ChatInput**: Input field with a send button.
- **ChatWindow**: Scrollable container for messages.
- **ThemeToggle**: Button to switch between light and dark mode.

### Setup

1. **Add the components**:
   - Copy the provided component files into `src/components/`.
   - Update `src/app/page.tsx` to include the `ChatWindow` and `ThemeToggle`.

2. **Update `globals.css`**:
   - Add CSS variables for dark mode colors.

3. **Run the app**:
   ```bash
   npm run dev
   ```
   - Open [http://localhost:3000](http://localhost:3000) to see the chat UI.

### Customization

- **Colors**: Edit the Tailwind classes or CSS variables in `globals.css`.
- **Layout**: Adjust the flexbox or grid layout in the component files.
- **Animations**: Add Framer Motion for smooth transitions.

---

## Model Verification

This template includes a GitHub Action that automatically verifies the C1 model used in `src/app/api/ask/route.ts` is valid according to the Thesys API. This workflow runs on every pull request to ensure you're using a supported model.

### Setting up the GitHub Action

To enable this workflow in your repository:

1. Go to your repository's **Settings** → **Secrets and variables** → **Actions**.
2. Add a new repository secret named `THESYS_API_KEY` with your Thesys API key value.
3. The workflow will now run automatically on all pull requests.

The workflow will:
- Extract the model name from `src/app/api/ask/route.ts`.
- Fetch the list of valid models from the Thesys API.
- Verify that your model is in the list of supported models.
- Block the PR from merging if an invalid model is detected.

You can view available models by running the verification script locally:

```bash
THESYS_API_KEY=<your-api-key> .github/scripts/verify-model.sh
```

### Making Model Verification Required (Recommended)

To require this check to pass before merging PRs:

1. Go to your repository's **Settings** → **Branches**.
2. Add or edit a branch protection rule for your main branch (e.g., `main` or `master`).
3. Enable **Require status checks to pass before merging**.
4. Search for and select **Verify C1 Model** in the status checks list.
5. Save the protection rule.

This ensures that only valid C1 models can be merged into your main branch.

---

## Learn More

To learn more about Thesys C1, take a look at the [C1 Documentation](https://docs.thesys.dev) - learn about Thesys C1.
