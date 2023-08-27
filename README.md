# file name zero remover written by UV-EAGLE
# a simple bash script to remove extra zeros in your file names. For example converting "filename0001" to "filename1". Run this script in the directory were the files reside and it will automatically detect file names that have exta zeros and remove the extra zeros in their names. 

#!/bin/bash
# Loop through all files in the current directory
for file in *; do
    if [[ -f "$file" ]]; then  # Check if the item is a regular file
        # Extract the basename and extension of the file
        filename=$(basename "$file")
        extension="${filename##*.}"
        basename="${filename%.*}"
        # Use regex to remove extra zeros before the number
        new_basename=$(echo "$basename" | sed -E 's/([a-zA-Z]+)0+([1-9][0-9]*)/\1\2/g')
        # Rename the file if the new basename is different from the old one
        if [[ "$basename" != "$new_basename" ]]; then
            new_filename="${new_basename}.${extension}"
            mv "$file" "$new_filename"
            echo "Renamed: $file -> $new_filename"
        fi
    fi
Done


