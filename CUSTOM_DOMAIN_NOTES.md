# Optional custom domain setup

If you own a domain, you can make the page look like:

https://melkoop.example.com

or:

https://www.melkoop.org

Steps:

1. Buy or use a domain you already own.
2. In your DNS provider, create a CNAME record:
   - Host/name: melkoop
   - Value/target: drchk.github.io
3. In GitHub:
   - Open the MelKoop repository
   - Go to Settings → Pages
   - Add your custom domain, for example: melkoop.example.com
   - Save
   - Enable HTTPS when GitHub allows it
4. GitHub will create or update a `CNAME` file in the repository.
