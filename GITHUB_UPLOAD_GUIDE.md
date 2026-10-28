# GitHub Upload Guide for PLV-VRS Frontend

## 1. Create the repository

1. Open https://github.com/new
2. Repository name: `plv-vrs-frontend`
3. Choose **Private** for the thesis project unless your group decides otherwise.
4. Do not initialize with a README, `.gitignore`, or license because these files are already included in the package.
5. Click **Create repository**.

## 2. Upload the project files

1. Extract `plv-vrs-frontend-upload.zip` on your computer.
2. Open the new GitHub repository.
3. Select **Add file → Upload files**.
4. Upload the extracted project contents, including the `.github` folder. Do not upload the ZIP file itself as the source code.
5. Commit the files directly to the `main` branch, or create a pull request if your group uses review branches.

## 3. Run it locally

Install Node.js 20+ and pnpm 10.12.4, then run:

```bash
pnpm install
pnpm dev
```

For the frontend-only prototype, leave `VITE_API_BASE_URL` empty. To connect the future Laravel API, copy `.env.example` to `.env` and set:

```env
VITE_API_BASE_URL=http://localhost:8000/api
```

Never upload `.env`, API tokens, Gemini keys, database passwords, or evidence files.

## 4. Confirm GitHub Actions

After the upload, open the repository's **Actions** tab. The `Frontend CI` workflow should run `pnpm typecheck` and `pnpm build` automatically on pushes and pull requests to `main` or `develop`.
