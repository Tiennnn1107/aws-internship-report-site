<h1 align="center">AWS Internship Report Site</h1>

<h3 align="center">
  A personal internship report website built with Hugo, Markdown, and the FCJ workshop template.
</h3>

<p align="center">
  <a href="https://github.com/tienhuu-dev/aws-internship-report-site">
    <img src="https://img.shields.io/badge/Repository-GitHub-181717?style=for-the-badge&logo=github" alt="GitHub repository" />
  </a>
  <img src="https://img.shields.io/badge/Hugo-0.137.1-FF4088?style=for-the-badge&logo=hugo" alt="Hugo version" />
  <img src="https://img.shields.io/badge/Status-In%20Development-0A66C2?style=for-the-badge" alt="Project status" />
</p>

---

## 👋 About This Repository

This repository contains a Hugo-based static website for documenting my AWS internship learning journey, technical progress, weekly reports, workshop practice, self-evaluation, and feedback.

The project is based on the FCJ workshop template and is customized as a personal report site for internship documentation.

---

## 🎯 Project Purpose

- Document internship progress in a structured format.
- Maintain weekly worklogs and learning outcomes.
- Present AWS-related workshop practice and technical notes.
- Keep a clean source branch for future GitHub Pages deployment.
- Provide mentors with a clear and reviewable report website.

---

## 🧑‍💻 Author

<h3 align="left">Hi 👋, I'm Tien Huu</h3>

- 🔭 I am currently working on **AWS Internship Report Site**.
- 🌱 I am currently learning **AWS, Hugo, GitHub Pages, and technical documentation**.
- 📝 I use this repository to document internship progress and cloud learning outcomes.
- 💻 GitHub: [tienhuu-dev](https://github.com/tienhuu-dev)
- 🔗 LinkedIn: [Tien Huu](https://www.linkedin.com/in/tien-huu-8a436a3a2)
- 📫 Email: [daohuutien2004@gmail.com](mailto:daohuutien2004@gmail.com)

---

## 🛠️ Technology Stack

![Hugo](https://img.shields.io/badge/Hugo-FF4088?style=for-the-badge&logo=hugo&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)

- **Static Site Generator:** Hugo Extended
- **Theme:** Hugo Learn Theme
- **Content Format:** Markdown
- **Version Control:** Git, GitHub
- **Deployment Target:** GitHub Pages

---

## 📚 Template Source

This project is based on the following FCJ workshop template:

```text
https://github.com/thienluhoan/fcj-workshop-template
```

The original template is kept as an upstream reference for future comparison or updates.

---

## ✅ Required Hugo Version

This template has compatibility constraints with newer Hugo versions. The confirmed working version is:

```text
hugo v0.137.1+extended windows/amd64
```

Recommended version:

```text
Hugo Extended v0.137.1
```

---

## 🚀 Local Development

Run the development server:

```powershell
hugo server -D
```

The website will be available at:

```text
http://localhost:1313/
```

---

## 🏗️ Build

Generate the static website:

```powershell
hugo
```

The generated output is written to:

```text
public/
```

The `public/` directory is ignored from the source branch because it is a generated build output.

---

## 🌿 Branch Strategy

| Branch | Purpose |
| --- | --- |
| `main` | Stable branch for reviewed code and future deployment. |
| `feature/site-foundation` | Development branch for preparing the report site foundation. |
| `backup/template-history` | Local backup branch that preserves the original template history. |

---

## 📁 Repository Structure

```text
.
├── archetypes/
├── content/
├── layouts/
├── static/
├── themes/
│   └── hugo-theme-learn/
├── config.toml
├── .gitignore
└── README.md
```

Main directories:

- `content/`: Markdown content for report sections.
- `layouts/`: Custom Hugo layout overrides.
- `static/`: Static assets such as images, CSS, and icons.
- `themes/`: Hugo theme used by the site.
- `config.toml`: Main Hugo site configuration.

---

## 🧭 Current Report Sections

The original template structure is currently preserved:

- Worklog
- Proposal
- Blogs Translated
- Events Participated
- Workshop
- Self-evaluation
- Feedback

These sections will be customized progressively to match the AWS internship report requirements.

---

## 🔗 Connect with Me

[![GitHub](https://img.shields.io/badge/GitHub-tienhuu--dev-181717?style=for-the-badge&logo=github)](https://github.com/tienhuu-dev)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Tien%20Huu-0A66C2?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/tien-huu-8a436a3a2)
[![Email](https://img.shields.io/badge/Email-daohuutien2004%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:daohuutien2004@gmail.com)

---

<p align="center">
  Built with ❤️ using Hugo and Markdown.
</p>
