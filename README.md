[![Build Status](https://cmchenry.visualstudio.com/wikidump/_apis/build/status/camchenry.wikidump?branchName=master)](https://cmchenry.visualstudio.com/wikidump/_build/latest?definitionId=1&branchName=master)

# wikidump

This crate processes Mediawiki XML dump files and turns them into easily
consumed pieces of data for language analysis, natural langauge processing,
and other applications.


# This fork includes
- Multi-stream decode support
- A progressbar
- Some minor performance fixes 

## Example
```rust
let parser = Parser::new()
    .use_config(config::wikipedia::english());

let site = parser
    .parse_file("tests/enwiki-articles-partial.xml")
    .expect("Could not parse wikipedia dump file.");

assert_eq!(site.name, "Wikipedia");
assert_eq!(site.url, "https://en.wikipedia.org/wiki/Main_Page");
assert!(!site.pages.is_empty());

for page in site.pages {
    println!("Title: {}", page.title);

    for revision in page.revisions {
        println!("\t{}", revision.text);
    }
}
```
