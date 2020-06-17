# Hunk format

The `@@ -1,7 +1,6 @@` piece in a git diff is not actually git specific, it
comes from GNU Diffutils and essentially means in the example above: "the hunk
starts on line 1, and is 7 line long for the original file, and starts on line
1 and is 6 line long for the new revision of the file."

Found in Building Git, section 12.3.1

Reference: https://www.gnu.org/software/diffutils/manual/diffutils.html#Detailed-Unified
