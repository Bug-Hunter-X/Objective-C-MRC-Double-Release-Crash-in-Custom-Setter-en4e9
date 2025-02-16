# Objective-C MRC Double Release Bug
This repository demonstrates a subtle bug in Objective-C's manual retain-release (MRC) memory management that can lead to a double release and application crash.  The issue stems from improper handling of object assignments within custom setter methods.

## The Bug
The core problem lies in the `setString:` method of `MyClass`. If the new string is identical to the existing string, the code mistakenly releases the string before assigning the new one, resulting in a double release when `dealloc` is eventually called.  This scenario is particularly insidious because it only occurs under specific circumstances, making it difficult to detect and debug.

## The Solution
The solution involves adding a check to ensure that a release only happens if the old string is different from the new string *and* not `nil`. This prevents accidental releases when assigning the same string.