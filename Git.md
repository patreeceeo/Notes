clone a repo but exclude all but a single branch: `git clone -b branch repo_url`

partial clone
1. `git clone --sparse --filter=blob:none --depth=1 <forkedUrl>`
    - `--sparse` initializes the sparse-checkout file so the working directory starts with only the files in the root of the repository.
    - `--filter=blob:none` will exclude files, fetching them only as needed.
    - `--depth=1` will further improve clone speed by truncating commit history, but it may cause issues as summarized [here](https://github.blog/2020-12-21-get-up-to-speed-with-partial-clone-and-shallow-clone/).
2. `git sparse-checkout add types/<type> types/<dependency-type> ...`