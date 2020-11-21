# Google Photos Takeout Fixer

## What is this, and why?

To get your Google Photos out, you can use Google Takeout. This is the best option since the API won't allow you to download the original files.

The Google Takeout result is a bit of a mess, resulting in:

- Duplicates of files, with them showing up in a directory for an album and the time based export.
- Incorrect binning of time - it seems to be based off the creation date rather than the files capture date.
- Missing creation/modification dates on your files - this information must come from EXIF or Google Photo's metadata.
- Google Photos metadata files for each file and directory.

This will:

- Double check the Google Photos times against EXIF metadata data (though assumes all your times are in one timezone so Google Photo's is likely more accurate)
- Detect photos with missing Google Photos metadata
- Detect photos with missing Google Photo's dates
- If exporting:
  - Recognise duplicate files for albums so you can choose which structure you prefer (a "Duplicates" directory gets created)
  - Re-organise photos into a year based directory structure, correctly based on the Google Photo's taken time
  - Set the file creation/modification date to the Google Photos taken time in your chosen timezone
  - Moves 'used' metadata to a "Metadata" directory
  - Keep a copy of any unused files so you can manually fix them or safely discard them (an "Unused" directory gets created)

__Disclaimers__

Admittedly the code is a bit of a mess! This was a useful tool for fixing up my own export but you may need to change it to suit your needs.

## Running

1. Ensure you have Ruby and bundler installed.
1. Install `libexif`, e.g.: `brew install libexif`
1. Run `bundle install`
1. Run `./fix_export` as `./fix_export scan_path check_exif time_zone [export_path]`

### Arguments

__scan_path__

This is the full path on your disk to scan from, exclude the `/` suffix.

__check_exif__

Set this to 'true' if you'd like to check a photo's internal metadata against Google Photos.

__time_zone__

The Ruby time zone to use for interpreting dates.

__export_path__ (optional)

The full file path to export clean files to on disk. This directory will be created if it doesn't exist.