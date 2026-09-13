# Auto Security Patcher

patches security stuff for economy sim / bubbablox / 2016-roblox-main ecs setups

## Requirements

- linux x86_64
- you dont need python, just run the exe
- your folder needs `2016-roblox-main` and usually `api` or `services/api`

## Usage

```bash
chmod +x auto-security-patcher
./auto-security-patcher /path/to/ecs --apply
```

dry run (just checks stuff, doesnt change files):

```bash
./auto-security-patcher /path/to/ecs --dry-run
```

after you patch rebuild the frontend:

```bash
cd /path/to/ecs/services/2016-roblox-main
npm run build && npm run start
```

check `security-hardening-report.json` in your ecs folder to see what got fixed

## What it does

basically runs through your ecs and fixes a bunch of common security holes in one go:

- removes discord webhook urls that got leaked in client files
- fixes login/password fields so theyre actually password inputs
- blocks eval/function/child_process stuff that can get you rce'd
- patches xss stuff like dangerouslySetInnerHTML and document.write
- closes debug/backdoor routes like /debug /__debug /internal
- fixes path traversal on sendFile and fs.readFile
- makes cookies more secure (httponly secure samesite)
- removes bad cors *, unsafe-inline csp, tls rejectUnauthorized false
- moves .env files out of public/ if someone put them there
- replaces hardcoded secrets with env vars
- adds security headers and a basic login rate limit
- saves everything to security-hardening-report.json

## What it does NOT do

- wont touch random projects that arent ecs
- doesnt mean youre 100% safe, test your site after
- doesnt do moderation or legal stuff for you thats on you

## Support

open a github issue if something breaks
