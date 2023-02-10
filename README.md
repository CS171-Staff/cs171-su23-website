# CS161 Website Template

## Creating website

At the start of a semester, follow these steps:

* Archive the previous semester's website.

    1. In Settings --> Options --> Github Pages on the duplicated repo, select the master branch, and set the custom domain to `sp20.cs161.org` (replacing `sp20` with the previous semester).

    2. Log into Namecheap (username is `cs161staff`, use the `cs161-staff@berkeley.edu` SPA email to password reset to access the account). Under Advanced DNS for `cs161.org`, add a CNAME Record mapping `sp20` to `cs161-staff.github.io` (replacing sp20 with the previous semester).

    3. Go back to Settings --> Options --> Github Pages, and check Enforce HTTPS when it becomes available.

    4. Remove any sensitive solutions from `assets`.

* Create a new website for this semester.

	1. [Create a repository from this template.](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/creating-a-repository-from-a-template)

	2. Update the schedule in `_data/schedule.yml`.

	3. Update the links in `_data/links.yml`.

	4. Update the link to the extensions form in `extensions.md`.

	5. Update staff in `_data/staff.yml`. Upload images to `assets/images/staff`.

	6. Ensure that the previous semester's exams and solutions are in `assets/exams`. Update `resources.md` to reflect the previous semester's exam and website. (TODO: We can probably find a way to integrate this with the template but I haven't worked it out yet. For now, manual merging isn't too bad.)

	7. If needed, update policies in `policies.md`.

## Maintaining website

Assignments, lectures, discussions, and announcements can all be found in the `schedule.yml` page.

## Building website

To publish to the world: push to master, and it will build automatically

To build locally: run `bundle exec jekyll serve`