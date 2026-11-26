# Math 4353 / 5353 Syllabi — Winter 2026–2027

One shared source builds two syllabi: Math 4353 (undergraduate) and Math 5353 (graduate). Content tagged `component="undergraduate"` appears only in the 4353 syllabus and content tagged `component="graduate"` only in the 5353 syllabus; everything else is common to both. Built from the syllabus template described below.

```sh
pretext build print-4353   # output/print-4353/MATH-4353-001_CLIFTON_W2027.pdf
pretext build print-5353   # output/print-5353/MATH-5353-001_CLIFTON_W2027.pdf
pretext build web-4353
pretext build web-5353
```

# Syllabus Template

This is a [PreTeXt](https://pretextbook.org/documentation.html) syllabus template for courses that use a weighted average grading scheme.

The course policies and student services sections are written for **Louisiana Tech University** — they cite University Policy 2206, the Louisiana Tech Academic Honor Code, and Louisiana Tech's counseling, disability, emergency-notification, help-desk, and tutoring resources. The template is usable elsewhere, but those sections (and the branding described under [Branding and personal defaults](#branding-and-personal-defaults)) have to be rewritten first.

## Layout

```
project.ptx              PreTeXt project manifest (web and print targets for each course)
publication/             One publication file per course: chunking, theme, and version flags
assets/                  Logos and favicons
source/
  main.ptx               Document root; XIncludes every section below
  course-vars.ent        Per-course entities (see below)
  docinfo.ptx            Brand logo
  frontmatter.ptx        Author, copyright, license
  contact_information/   Instructor info, office hours, email etiquette
  course_information/    Description, topics, prerequisites, SLOs, methods
  evaluation/            Weights, grading scale, exams, homework, quizzes, engagement
  course_policies/       Textbook, attendance, late work, make-ups, honor code
  student_services/      Disability, counseling, ENS, withdrawal, LMS help, tutoring
```

## Customizing the syllabus

Most per-course details are defined as entities in [`source/course-vars.ent`](source/course-vars.ent). Edit the values there to set:

- the undergraduate and graduate course numbers, section, term, and year;
- the instructor's honorific, first and last name, phone, email, website, and office;
- the department and institution (used on the title page);
- the textbook title, author, edition, and ISBN;
- the midterm exam date, the final exam date, and the drop-with-a-`W` deadline.

Each value is reused everywhere the corresponding entity appears, so editing it in one place updates every section that references it.

The remaining placeholder prose should be filled in directly in the corresponding files under `source/`:

| File | Contains |
| --- | --- |
| [`course_information/course_description.ptx`](source/course_information/course_description.ptx) | Course description |
| [`course_information/course_topics.ptx`](source/course_information/course_topics.ptx) | Course topics |
| [`course_information/prereqs.ptx`](source/course_information/prereqs.ptx) | Prerequisites |
| [`course_information/student_learning_outcomes.ptx`](source/course_information/student_learning_outcomes.ptx) | Student learning outcomes |
| [`course_information/instructional_methods.ptx`](source/course_information/instructional_methods.ptx) | Delivery mode (defaults to face-to-face lecture) |
| [`contact_information/office_hours.ptx`](source/contact_information/office_hours.ptx) | Office-hour days and times |
| [`evaluation/weights.ptx`](source/evaluation/weights.ptx) | Grade categories and weights (defaults: homework 25%, quizzes and engagement 15%, midterm 25%, final 35%) |
| [`evaluation/grading_scale.ptx`](source/evaluation/grading_scale.ptx) | Letter-grade cutoffs (defaults to a straight 90/80/70/60 scale) |

The evaluation and policy sections (`exams.ptx`, `homework.ptx`, `quizzes.ptx`, `engagement.ptx`, `late.ptx`, `attendance.ptx`, `make-up.ptx`) ship with working default prose. Read them before publishing — they state specific policies, such as late work not being accepted and academic dishonesty resulting in a grade of F for the course.

### Branding and personal defaults

A few values are hard-coded rather than driven by entities. Change them when adopting the template:

- [`source/frontmatter.ptx`](source/frontmatter.ptx) — copyright holder and years.
- [`source/docinfo.ptx`](source/docinfo.ptx) — the brand logo and the URL it links to.
- [`assets/images/`](assets/images) — the Louisiana Tech logos, including `logo.png` referenced by `docinfo.ptx`.
- [`publication/publication-4353.ptx`](publication/publication-4353.ptx) and [`publication/publication-5353.ptx`](publication/publication-5353.ptx) — the HTML theme and its primary colors (currently the `boulder` theme in Louisiana Tech blue and red).

## Building

This is a standard PreTeXt project; [`requirements.txt`](requirements.txt) pins the PreTeXt-CLI version to build with. With the CLI installed:

```sh
pip install -r requirements.txt
pretext build          # build the default target (web-4353)
pretext view           # preview in a browser
```

[`project.ptx`](project.ptx) defines four targets: `web-4353` and `web-5353` (HTML), and `print-4353` and `print-5353` (PDF). Build one at a time with `pretext build print-4353`, and so on. See the [PreTeXt documentation](https://pretextbook.org/documentation.html) for installation and deployment details.

Two conveniences come with the repo:

- [`.devcontainer.json`](.devcontainer.json) lets the project be edited and built in GitHub Codespaces without a local install.
- [`.github/workflows/pretext-cli.yml`](.github/workflows/pretext-cli.yml) builds the project on every pull request (and on demand via *Run workflow*), uploading the staged site as an artifact. It also deploys to Cloudflare Pages when the `CLOUDFLARE_PROJECT_NAME` repository variable is set, and to GitHub Pages when `PTX_ENABLE_DEPLOY_GHPAGES` is `yes` and the run is on the default branch. Building on pushes to `main` is commented out in that file.

## Optional sections (version flags)

Several sections are conditional. They are tagged in the source with a `component` attribute and are only rendered when that component is listed in the `<version include="…"/>` element in the course's publication file. To turn a section on or off, add or remove its flag from that list in both publication files.

| Flag | Controls |
| --- | --- |
| `undergraduate` | Math 4353 course number and point totals. Listed only in `publication-4353.ptx`. |
| `graduate` | Math 5353 course number and point totals, the extra exam and homework problems, and the excursion report and presentation. Listed only in `publication-5353.ptx`. |
| `exams` | Exams section and make-up policy. |
| `engagement` | Graded participation/engagement. |
| `homework` | Homework section. |
| `quizzes` | Quizzes section. |
| `BARC` | BARC university tutoring resources. |
| `mathclub` | Math Club tutoring resources. |

`BARC` and `mathclub` are off by default; enable them only for service-level courses where tutoring is available through those resources.

Turning a section off hides its prose but not its weight — remove the matching row from [`evaluation/weights.ptx`](source/evaluation/weights.ptx) as well, and adjust the remaining weights so they still total 100%.

## License

This work is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/). See [`LICENSE`](LICENSE) for the full text.
