git init
git branch -M main
git remote remove origin 2>/dev/null || true
git remote add origin https://github.com/9jkdbpb967-spec/AMC-intelligence-.git

git add .
git commit -m "Add AMC-EOS v10.52 First-Green Hardened"

git pull origin main --rebase
git push -u origin main
