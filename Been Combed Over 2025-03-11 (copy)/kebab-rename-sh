#!/bin/bash

# Function to convert string to kebab-case
to_kebab_case() {
    echo "$1" | 
    # Convert to lowercase
    tr '[:upper:]' '[:lower:]' | 
    # Replace spaces and special characters with hyphens
    sed 's/[^a-z0-9]\+/-/g' |
    # Remove leading/trailing hyphens
    sed 's/^-*\|-*$//g'
}

# Function to rename files and directories
rename_items() {
    local dir="$1"
    
    # Find all files and directories in current directory, process depth-first
    find "$dir" -depth | while read -r item; do
        # Skip if it's the script itself or current directory
        [ "$item" = "$0" ] || [ "$item" = "." ] || [ "$item" = "$dir" ] && continue
        
        # Get the directory path and filename separately
        dir_path=$(dirname "$item")
        old_name=$(basename "$item")
        
        # Convert to kebab-case
        new_name=$(to_kebab_case "$old_name")
        
        # Skip if no change would be made
        [ "$old_name" = "$new_name" ] && continue
        
        # Construct full new path
        new_path="$dir_path/$new_name"
        
        # Check if target already exists
        if [ -e "$new_path" ]; then
            echo "Warning: Skipping '$item' -> '$new_path' (target already exists)"
            continue
        fi
        
        # Rename the item
        mv -v "$item" "$new_path"
    done
}

# Start renaming from current directory
echo "Starting rename operation..."
echo "Converting all names to lowercase kebab-case"
echo

rename_items "$(pwd)"

echo
echo "Rename operation completed!"