# Semantic Versioning library

Create and manage software version information according to the [Semantic Versioning specification][semver]. `SemanticVersion` objects will validate against, and compare to, anything resembling a semantic version String after conversion (“resembling” because trailing 0s can be omitted, i.e. “4” will be equivalent to “4.0.0”):

```ruby
version = SemanticVersion.new('1.5.4+b217')
version.major                                              # => 1
version.minor                                              # => 5
version.patch                                              # => 4
version.metadata                                           # => "b217"
                                                           
# String conversions                                       
version.to_s                                               # => "1.5.4"
version.to_gem_version                                     # => "1.5.4"
version.to_str                                             # => "1.5.4+b217"
version.to_full_version                                    # => "1.5.4+b217"
                                                           
# Other conversions                                        
version.to_a                                               # => [1, 5, 4]
version.to_hash                                            # => {major: 1, minor: 5, patch: 4}
version.to_version                                         # => SemanticVersion
```

SemanticVersion objects are comparable to anything that `SemanticVersion.new()` accepts:

```ruby
SemanticVersion.new('1.1.2') < 1.2                         # => true
SemanticVersion.new(1.2) == '1.2.0'                        # => true
SemanticVersion.new(1) > SemanticVersion.new('2.19')       # => false
```

Build and prerelease metadata is retained, but, [as specified][semver], only the prerelease status is used in comparisons:

```ruby
bld = SemanticVersion.new('2.0+b.212')
bld.metadata                                               # => "b.212"
bld.prerelease?                                            # => false
bld == '2.0.0'                                             # => true
                                                           
pre = SemanticVersion.new('2.0-pre.1')                     
pre.metadata                                               # => "pre.1"
pre.prerelease?                                            # => true
pre  < 2                                                   # => true
```

SemanticVersion object versions can be bumped in a spec conforming fashion:

```ruby
SemanticVersion.new('1.1.2').bump.to_full_version          # => "1.1.3"
SemanticVersion.new('1.1.2').bump(:minor).to_full_version  # => "1.2.0"
SemanticVersion.new('1.1.2').bump(:major).to_full_version  # => "2.0.0"
                                                           
with_pre_info = SemanticVersion.new('1.0-pre')             
with_pre_info.to_full_version                              # => "1.0.0-pre"
with_pre_info.bump(:minor).to_full_version                 # => "1.1.0"
```

## License

Code licensed under the BSD License (see *LICENSE* file).

[semver]:  http://semver.org/
[semver2]: http://rubygems.org/gems/semver2 
[semantic_versioning]: http://rubygems.org/gems/semantic_versioning
