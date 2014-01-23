# Semantic Versioning library

Create and manage software version information according to the [Semantic Versioning specification][semver]. `SemanticVersion` objects will validate against, and compare to, anything resembling a semantic version String after conversion (“resembling” because trailing 0s can be omitted, i.e. “4” will be equivalent to “4.0.0”):

```ruby
SemanticVersion.new('1.1.2') < 1.2                   # => true
SemanticVersion.new(1.2) == '1.2.0'                  # => true
SemanticVersion.new('2.0+b.212') == '2.0.0'          # => true
SemanticVersion.new('2.0-pre.1') < 2                 # => true
SemanticVersion.new(1) > SemanticVersion.new('2.19') # => false
```
Note build and prerelease metadata is retained, but not used in comparisons.

SemanticVersion versions can be bumped in a spec conforming fashion:

```ruby
SemanticVersion.new('1.1.2').bump.to_full_version         # => "1.1.3"
SemanticVersion.new('1.1.2').bump(:minor).to_full_version # => "1.2.0"
SemanticVersion.new('1.1.2').bump(:major).to_full_version # => "2.0.0"
with_pre_info = SemanticVersion.new('1.0-pre')
with_pre_info.to_full_version                             # => "1.0.0-pre"
with_pre_info.bump(:minor).to_full_version                # => "1.1.0"
```

[semver]: http://semver.org/
