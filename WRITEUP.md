# Project Write-up: Deploy an Article CMS to Azure

## Resource Justification

### VM vs App Service

| Criteria        | VM                                           | App Service                                    |
|----------------|-----------------------------------------------|------------------------------------------------|
| **Cost**       | Higher due to full OS and compute management | Lower with per-second billing and scaling     |
| **Scalability**| Manual setup for scaling and load balancing  | Auto-scaling supported by Azure natively      |
| **Availability**| Requires configuration for HA                | High availability out-of-the-box              |
| **Workflow**   | More flexible, but complex deployment        | Streamlined with GitHub Actions & CI/CD      |

### Final Choice: ✅ Azure App Service

**Justification**:  
App Service is the better fit for this CMS because it supports:
- GitHub-based CI/CD
- Auto-scaling
- Lower cost for hosting a Flask app
- Simple integration with Microsoft Identity and Azure services

If the app required custom OS control, low-level access, or persistent background jobs, VM would be a better fit.

---

## App Changes Supporting the Decision

To support App Service deployment:
- The app was containerized into a Flask structure.
- GitHub Actions were added to automate CI/CD.
- ProxyFix middleware was added to support HTTPS redirects in App Service.
- MSAL was used to integrate with Azure AD using App registration.

---

## SQL + Storage Setup

- A SQL Server and database named `cms` was created.
- Tables `posts` and `users` were added.
- Azure Blob Storage was created and connected using the container `images`.

### Connection strings were added to App Service:
- `SQL_CONNECTION_STRING`
- `AZURE_STORAGE_CONNECTION_STRING`

---

## Deployment Verification

### ✅ Python Web App:
- Deployed via GitHub Actions
- CI/CD logs confirmed successful deployment

### ✅ SQL:
- Azure SQL Server: `cms-sql-narjes.database.windows.net`
- Tables created: `users`, `posts`

### ✅ Blob Storage:
- Storage account: `stnarjes`
- Container: `images`
- Image URL displayed in `/home`

---

## Security & Monitoring

- MSAL library used to implement **Sign in with Microsoft**
- Redirect URI: `https://web-fask-app-hffxh6brdresfng7.westus-01.azurewebsites.net/getAToken`
- App registration configured with correct redirect URI and client secret

### Logging:
- Errors and login attempts were captured using:
  - Flask internal logs
  - Azure Log Stream

---

## Bonus Features

✅ Subtitle field was added in DB and UI  
✅ Microsoft login integrated  
✅ Admin user tracking via Microsoft claims  
✅ Image storage and serving via blob container

---

## Author

- Name: Narjes Mishal Alkhars  
- Date: June 6, 2025  
- App URL: https://web-fask-app-hffxh6brdresfng7.westus-01.azurewebsites.net

---

🎉 **Project Complete!**
🎉 **helo nanodegree!!!!!**
