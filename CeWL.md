# CeWL (Custom Word List Generator)

## What is it?
CeWL is a Ruby-based tool that spiders a website and generates a custom 
wordlist by extracting words found on the pages. It's commonly used in 
password attacks (e.g., building a targeted wordlist for brute-forcing 
or dictionary attacks) since people often base passwords on words related 
to a company, product, or personal info found on a site.

## Basic Syntax
```bash
cewl [options] <url>
```

## Common Options

| Flag | Description |
|------|-------------|
| `-d <depth>` | Depth to spider the site (default: 2) |
| `-m <min_length>` | Minimum word length to include |
| `-w <output_file>` | Write wordlist to a file |
| `-e` | Include email addresses found on the site |
| `--email_file <file>` | Write found emails to a separate file |
| `-a` | Include metadata (author info from documents) |
| `-c` | Show word count |
| `-v` | Verbose mode |
| `-u <user-agent>` | Set a custom user-agent |
| `--with-numbers` | Include words containing numbers |

## Example Usage

**Basic wordlist generation:**
```bash
cewl http://example.com -w wordlist.txt
```

**Spidering deeper with minimum word length:**
```bash
cewl -d 3 -m 5 http://example.com -w wordlist.txt
```

**Extracting emails along with words:**
```bash
cewl -e --email_file emails.txt http://example.com -w wordlist.txt
```

**Verbose output with word count:**
```bash
cewl -v -c http://example.com
```

## Use Case in eJPT
- After identifying a target web application, run CeWL against it to 
  build a custom wordlist based on site-specific terminology.
- Combine this wordlist with tools like Hydra or John the Ripper for 
  targeted password attacks instead of relying solely on generic 
  wordlists like rockyou.txt.
- Useful when default wordlists fail and you suspect passwords are 
  related to company names, products, or staff names found on the site.

## Notes
- CeWL
