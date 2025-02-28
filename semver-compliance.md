# SemVer Compatibility

Below is the SemVer 2.0.0 specification, omitting examples, as taken from [semver.org](https://semver.org/).

Compliance that depends on a workaround or "hack" is marked with a character:

- `*` = only compliant by using the "skip" workaround:
  > If you don't publish a release every month, it is perfectly fine to "skip" versions.<br>
  > This question has been asked and answered multiple times:
  > - https://github.com/semver/semver/issues/233
  > - https://github.com/semver/semver/issues/942
  > - https://github.com/semver/semver/pull/393
- `†` = only compliant by using the "yearly zero" workaround.
  To quote from our FAQ: 
  > If you don't want to skip "zero" versions, a good yearly "zero" is updating any mentions of the year in the codebase, like copyright notices or "is maintained" badges.<br>
  > For instance https://shields.io/badges/maintenance: !["is maintained" badge](https://img.shields.io/maintenance/yes/2025)
- `‡` = only compliant by using the "0." prefix workaround
  > It can be made _compliant_ by **only** breaking backward compatibility once a year, every year.<br>
  > An alternative is to prefix the version with a `0` so you're allowed to whatever you want, as per spec. (e.g. `0.24.3`)

- `⸸` = only compliant by breaking backward compatibility _only once_ a year, _every_ year.

## SemVer 2.0.0 compliance

1. - Software using Semantic Versioning MUST declare a public API.
   - This API could be declared in the code itself or exist strictly in documentation.
   - However it is done, it SHOULD be precise and comprehensive.
2. - A normal version number MUST take the form X.Y.Z where X, Y, and Z are non-negative integers,
   - and MUST NOT contain leading zeroes.
   - X is the major version, Y is the minor version, and Z is the patch version.
   - Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.
3. - Once a versioned package has been released, the contents of that version MUST NOT be modified.
   - Any modifications MUST be released as a new version.
4. - Major version zero (0.y.z) is for initial development.
   - Anything MAY change at any time.
   - The public API SHOULD NOT be considered stable.
5. - Version 1.0.0 defines the public API.<sup>* or ‡</sup>
   - The way in which the version number is incremented after this release is dependent on this public API and how it changes.
6. - Patch version Z (x.y.Z \| x > 0) MUST be incremented if only backward compatible bug fixes are introduced.<sup>* or ‡</sup>
   - A bug fix is defined as an internal change that fixes incorrect behavior.
7. - Minor version Y (x.Y.z \| x > 0) MUST be incremented if new, backward compatible functionality is introduced to the public API.<sup>* or ‡</sup>
   - It MUST be incremented if any public API functionality is marked as deprecated.
   - It MAY be incremented if substantial new functionality or improvements are introduced within the private code.
   - It MAY include patch level changes.
   - Patch version MUST be reset to 0 when minor version is incremented.<sup>*</sup>
8. - Major version X (X.y.z \| X > 0) MUST be incremented if any backward incompatible changes are introduced to the public API.<sup>‡ or ⸸</sup>
   - It MAY also include minor and patch level changes.
   - Patch and minor versions MUST be reset to 0 when major version is incremented.<sup>* or †</sup>
9. - A pre-release version MAY be denoted by appending a hyphen and a series of dot separated identifiers immediately following the patch version.
   - Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-].
   - Identifiers MUST NOT be empty.
   - Numeric identifiers MUST NOT include leading zeroes.
   - Pre-release versions have a lower precedence than the associated normal version.
   - A pre-release version indicates that the version is unstable and might not satisfy the intended compatibility requirements as denoted by its associated normal version.
10. - Build metadata MAY be denoted by appending a plus sign and a series of dot separated identifiers immediately following the patch or pre-release version. Identifiers MUST comprise only ASCII alphanumerics and hyphens [0-9A-Za-z-]. Identifiers MUST NOT be empty. Build metadata MUST be ignored when determining version precedence. Thus two versions that differ only in the build metadata, have the same precedence.
11. - Precedence refers to how versions are compared to each other when ordered.
    1. - Precedence MUST be calculated by separating the version into major, minor, patch and pre-release identifiers in that order (Build metadata does not figure into precedence).
    2. - Precedence is determined by the first difference when comparing each of these identifiers from left to right as follows: Major, minor, and patch versions are always compared numerically.
    3. - When major, minor, and patch are equal, a pre-release version has lower precedence than a normal version:
    4. - Precedence for two pre-release versions with the same major, minor, and patch version MUST be determined by comparing each dot separated identifier from left to right until a difference is found as follows:

         1. Identifiers consisting of only digits are compared numerically.
         2. Identifiers with letters or hyphens are compared lexically in ASCII sort order.
         3. Numeric identifiers always have lower precedence than non-numeric identifiers.
         4. A larger set of pre-release fields has a higher precedence than a smaller set, if all of the preceding identifiers are equal.
