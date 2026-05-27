# B.S. Bharath Saiguhan, CV

Here is where I keep my (hopefully updated) CV, publication list, talks, etc.

For more information on my research, please visit my personal homepage: [bsaiguhan.net](https://bsaiguhan.net)

Pdf files can be accessed using the links below:

- [**Full CV**](https://github.com/bsgalvan/cv-auto/releases/latest/download/BharathSaiguhan_fullCV.pdf)
- [**Short CV**](https://github.com/bsgalvan/cv-auto/releases/latest/download/BharathSaiguhan_shortCV.pdf)
- [**Publication list**](https://github.com/bsgalvan/cv-auto/releases/latest/download/BharathSaiguhan_publist.pdf)
- [**Talk list**](https://github.com/bsgalvan/cv-auto/releases/latest/download/BharathSaiguhan_talklist.pdf)

### My CV and website workflow

This is how I handle it. 

The only files one needs to change are `database.py` and `CV.tex`. Everything else is machine-generated.

- Add new papers, talks, and students in `database.py` in the same format as the others. The order is important.
- Touch the other things in the CV directly in `CV.tex`.
- Tags `%mark_CVshort` indicate what to exclude when building the short version of the CV.

The script `makeCV.py` does the following:

- Fetch citations from [ADS](https://davidegerosa.com/myads) and [INSPIRE](https://davidegerosa.com/myinspire).
- Put together papers and talks in tex format.
- Fetch full bibtex record from [ADS](https://davidegerosa.com/myads) for a `.bib` file.
- Create markdown pages `_*.md` for a static website like [my own](https://bsaiguhan.net).
- Sanitize the database if the ADS key changed.
- Push to git (optional, only if run locally)

Then there's a github action `.github/workflows/cv-auto_website.yml` that:

- Run `makeCV.py` (requires `ADS_TOKEN` as a repository secret).
- Compile full CV, short CV, standalone publication list, standalone presentation list.
- Publish a [Github release](https://github.com/bsgalvan/cv-auto/releases) to get permanent URLs.
- Push updates to the [CV repo](https://github.com/bsgalvan/cv-auto) if any.
- Push updates to the [website repo](https://github.com/bsgalvan/website) if any (from there, another action will publish the website itself).
- (The action runs in a Docker image created by another action; that's to avoid re-installing latex every single time)


At the end of the day: you change something in `database.py` or `CV.tex`, and commit.
