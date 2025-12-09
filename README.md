# Version

Generic Resume Version: v0.0.3
SoftwareEngineering Resume Version: v0.0.6

# Portfolio & Resume


![2](https://github.com/user-attachments/assets/7aa66053-5aa8-4e4d-8244-4a893fab946d)



This repository currently hosts my professional resume along with an automated workflow that compiles and releases it as a LaTeX-generated PDF. While it presently focuses on my resume, I plan to expand this repository with more projects and content in the future.

## Resume

- **Directory:** `Resume/`
- **Description:** Contains multiple LaTeX resume variants optimized for different purposes.
- **Structure:**
  - `Resume/Generic/` - General-purpose resume with all experience
  - `Resume/SoftwareEngineering/` - Software Engineering role-focused resume
- **GitHub Action:** An automated workflow detects changes, compiles only modified variants, and publishes them as separate releases with independent versioning.
- **Usage:** Update the LaTeX files in the specific variant directory (e.g., `Resume/SoftwareEngineering/Resume.tex`); the GitHub Action will compile that variant, increment its version, and create a tagged release (e.g., `softwareengineering-v0.0.2`).

## Future Plans

I plan to add more projects and portfolio items to this repository. For now, it serves as the central location for my resume and its automated release process.

## Getting Started

1. **Clone the Repository**
   ```bash
   git clone https://github.com/rohanbatrain/Portfolio.git
   ```
2. **Navigate to the Resume Directory**
   ```bash
   cd Portfolio/Resume
   ```
3. **Update and Customize**
   - Edit the LaTeX files in the specific variant directory (e.g., `Resume/Generic/Resume.tex`)
   - The GitHub Action will automatically detect changes, compile only modified variants, increment their versions, and create separate tagged releases.

## Contributing

Contributions, suggestions, and improvements are welcome! Feel free to open an issue or submit a pull request if you have ideas to enhance this repository.

## License

This repository is available for personal and educational use. For any commercial use or additional inquiries, please contact me directly.

## Contact

For questions, feedback, or further information, please open an issue or reach out via my GitHub profile.
