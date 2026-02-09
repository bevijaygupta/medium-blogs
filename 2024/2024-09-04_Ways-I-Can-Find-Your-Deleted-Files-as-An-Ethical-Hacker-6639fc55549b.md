---
title: "Ways I Can Find Your Deleted Files as An Ethical Hacker 6639fc55549b"
platform: Medium
original_file: 2024-09-04_Ways-I-Can-Find-Your-Deleted-Files-as-An-Ethical-Hacker-6639fc55549b.md
---

# Ways I Can Find Your Deleted Files as An Ethical Hacker 6639fc55549b

::: {}
# Ways I Can Find Your Deleted Files as An Ethical Hacker {#ways-i-can-find-your-deleted-files-as-an-ethical-hacker .p-name}
:::

::: {.section .p-summary field="subtitle"}
In the digital age, the privacy of our data has never been more
critical. Whether you accidentally delete a file or purposely erase
it...
:::

::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#1807 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Ways I Can Find Your Deleted Files as An Ethical Hacker {#8d18 .graf .graf--h3 .graf--leading .graf--title name="8d18"}

<figure id="597d" class="graf graf--figure graf-after--h3">
<img src="https://cdn-images-1.medium.com/max/800/0*iHx11HLClIUxTv2Q"
class="graf-image" data-image-id="0*iHx11HLClIUxTv2Q" data-width="480"
data-height="270" />
</figure>

In the digital age, the privacy of our data has never been more
critical. Whether you accidentally delete a file or purposely erase it,
there's always a lingering question: Is it truly gone? As an ethical
hacker, I can reveal that even deleted files can often be recovered with
the right tools and techniques. This blog will walk you through various
methods to retrieve deleted files, explore how these techniques work,
and offer code snippets to demonstrate the processes.
:::
::::
::::::

:::::: {#1571 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Understanding File Deletion {#ec26 .graf .graf--h3 .graf--leading name="ec26"}

Before diving into recovery techniques, it's crucial to understand what
happens when a file is deleted. In most cases, deleting a file doesn't
erase its content from the hard drive. Instead, the operating system
removes the file's entry from the file system directory, marking the
space as available for new data. Until that space is overwritten by new
information, the original file data remains on the disk and can often be
recovered.
:::
::::
::::::

:::::: {#48fc .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Method 1: Using Data Recovery Software {#84f5 .graf .graf--h3 .graf--leading name="84f5"}

One of the most straightforward ways to recover deleted files is by
using specialized data recovery software. These tools scan the disk for
recoverable data and attempt to reconstruct the original files.

#### Steps to Recover Deleted Files Using Data Recovery Software {#984f .graf .graf--h4 .graf-after--p name="984f"}

1.  [**Install Data Recovery Software:** Popular tools include Recuva,
    EaseUS Data Recovery Wizard, and Disk Drill. These are user-friendly
    and capable of recovering a wide range of file types.]{#f229}
2.  [**Scan the Disk:** Once installed, launch the software and select
    the disk or partition where the file was located before deletion.
    Initiate the scan, and the software will search for recoverable
    files.]{#89df}
3.  [**Preview and Recover:** After the scan, the software will display
    a list of recoverable files. You can preview these files to ensure
    they are intact. Select the ones you wish to recover and save them
    to a different location to avoid overwriting any remaining
    data.]{#7332}

#### Code Example Using Python's OS and Shutil Modules {#0bf7 .graf .graf--h4 .graf-after--li name="0bf7"}

While the code example here is simplified, it demonstrates how one could
search for deleted files using Python.

``` {#e894 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import os
import shutil
```

``` {#f860 .graf .graf--pre .graf-after--pre}
def search_deleted_files(directory):
    deleted_files = []
    for root, dirs, files in os.walk(directory):
        for file in files:
            if file.startswith('~'):  # Placeholder for deleted files
                deleted_files.append(os.path.join(root, file))
    return deleted_files
```

``` {#f174 .graf .graf--pre .graf-after--pre}
def recover_files(deleted_files, recovery_dir):
    if not os.path.exists(recovery_dir):
        os.makedirs(recovery_dir)
    for file in deleted_files:
        shutil.copy(file, recovery_dir)
```

``` {#75d9 .graf .graf--pre .graf-after--pre}
# Usage
directory_to_search = 'C:/Users/YourUsername/Documents'
recovery_directory = 'C:/RecoveredFiles'
```

``` {#fd6b .graf .graf--pre .graf-after--pre}
deleted_files = search_deleted_files(directory_to_search)
recover_files(deleted_files, recovery_directory)
```

``` {#86ba .graf .graf--pre .graf-after--pre}
print(f'Recovered {len(deleted_files)} files to {recovery_directory}')
```

This script is highly simplified and would require more sophistication
to handle real-world file recovery.
:::
::::
::::::

:::::: {#12e6 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Method 2: File Carving {#e8dd .graf .graf--h3 .graf--leading name="e8dd"}

File carving is a more advanced technique that involves recovering files
based on their file structure and content, without relying on the file
system's metadata. This method is often used when the file system is
corrupted, or the metadata has been destroyed.

#### Steps to Perform File Carving {#3924 .graf .graf--h4 .graf-after--p name="3924"}

1.  [**Disk Imaging:** Create a bit-by-bit copy of the disk to avoid
    altering the original data during recovery. Tools like
    `dd`{.markup--code .markup--li-code} (on Unix systems) or FTK Imager
    can be used for this purpose.]{#b872}
2.  [**Carve Files:** Use a file carving tool like Foremost or Scalpel.
    These tools scan the disk image for file signatures and try to
    reconstruct the files.]{#a973}
3.  [**Analyze Recovered Files:** Once the carving process is complete,
    the files can be analyzed to determine their integrity.]{#fb48}

#### Example Using Foremost (Command Line Tool) {#bacd .graf .graf--h4 .graf-after--li name="bacd"}

Foremost is a command-line tool that can recover deleted files by
scanning for known file headers and footers.

``` {#b8d4 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
sudo foremost -i /path/to/disk/image.dd -o /path/to/output/folder
```

This command will scan the disk image and recover any files it can
identify, saving them in the specified output folder.

#### Python Code for Basic File Carving {#5ca2 .graf .graf--h4 .graf-after--p name="5ca2"}

Below is a very basic implementation of file carving using Python. It
focuses on identifying JPEG files from a disk image.

``` {#f4d8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="python"}
def file_carving(image_file, output_dir):
    with open(image_file, 'rb') as img:
        data = img.read()
```

``` {#e7b5 .graf .graf--pre .graf-after--pre}
    start_marker = b'\xff\xd8'  # JPEG start
    end_marker = b'\xff\xd9'    # JPEG end
    counter = 0
```

``` {#e0cd .graf .graf--pre .graf-after--pre}
    start = data.find(start_marker)
    while start != -1:
        end = data.find(end_marker, start) + 2
        jpeg_data = data[start:end]
```

``` {#7038 .graf .graf--pre .graf-after--pre}
        with open(f'{output_dir}/recovered_{counter}.jpg', 'wb') as f:
            f.write(jpeg_data)
```

``` {#79a2 .graf .graf--pre .graf-after--pre}
        counter += 1
        start = data.find(start_marker, end)
```

``` {#b6b7 .graf .graf--pre .graf-after--pre}
    print(f'Recovered {counter} JPEG files.')
```

``` {#9c27 .graf .graf--pre .graf-after--pre}
# Usage
image_file_path = 'disk_image.dd'
output_directory = 'RecoveredImages'
```

``` {#c939 .graf .graf--pre .graf-after--pre}
file_carving(image_file_path, output_directory)
```

This code snippet is for illustrative purposes and should be expanded
for use in a real-world scenario.
:::
::::
::::::

:::::: {#e61a .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Method 3: Analyzing the File System {#d4fb .graf .graf--h3 .graf--leading name="d4fb"}

Another method to recover deleted files involves directly analyzing the
file system structures. This method requires an understanding of how
file systems manage data and the ability to interpret low-level disk
structures.

#### Steps to Analyze the File System {#06c9 .graf .graf--h4 .graf-after--p name="06c9"}

1.  [**Understand the File System:** Different file systems (e.g., NTFS,
    FAT32, ext4) manage data differently. Understanding these
    differences is crucial for effective recovery.]{#58a6}
2.  [**Use a Hex Editor:** Tools like `HxD`{.markup--code
    .markup--li-code} or `WinHex`{.markup--code .markup--li-code} can be
    used to view and manipulate raw disk data. By analyzing the file
    system metadata (e.g., the Master File Table in NTFS), you can
    locate and recover deleted files.]{#4243}
3.  [**Recover the Files:** Once the location of the deleted file is
    identified, it can be reconstructed by copying the corresponding
    data blocks to a new file.]{#3b6e}

#### Example Using Python and Pytsk3 {#e8a1 .graf .graf--h4 .graf-after--li name="e8a1"}

The `pytsk3`{.markup--code .markup--p-code} library in Python allows
interaction with the file system and can be used for file recovery.

``` {#8ce6 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="cpp"}
import pytsk3
import pyewf
```

``` {#90cf .graf .graf--pre .graf-after--pre}
def open_image(image_path):
    image = pytsk3.Img_Info(image_path)
    return image
```

``` {#3a78 .graf .graf--pre .graf-after--pre}
def list_files(img, path="/"):
    fs = pytsk3.FS_Info(img)
    directory = fs.open_dir(path)
    
    for entry in directory:
        if entry.info.name.name in [".", ".."]:
            continue
        print(entry.info.name.name)
```

``` {#c879 .graf .graf--pre .graf-after--pre}
# Usage
image_file_path = 'path_to_disk_image.img'
image = open_image(image_file_path)
list_files(image)
```

This script lists the files in a directory of a disk image. By expanding
this code, you can recover deleted files by examining the file system
metadata.
:::
::::
::::::

:::::: {#caa6 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Method 4: Analyzing Unallocated Space {#cb14 .graf .graf--h3 .graf--leading name="cb14"}

Unallocated space on a disk is the area that the file system reports as
free. However, until this space is overwritten by new data, it might
still contain remnants of deleted files.

#### Steps to Analyze Unallocated Space {#89be .graf .graf--h4 .graf-after--p name="89be"}

1.  [**Extract Unallocated Space:** Tools like `Autopsy`{.markup--code
    .markup--li-code} or `The Sleuth Kit (TSK)`{.markup--code
    .markup--li-code} can be used to extract unallocated space from a
    disk image.]{#a9cb}
2.  [**Search for File Fragments:** The unallocated space can then be
    searched for file fragments, which can be reconstructed into usable
    files.]{#c084}
3.  [**Reconstruct Files:** If enough of the file's data is found, it
    can be reconstructed and recovered.]{#aaf0}

#### Example Using Sleuth Kit's fls and icat {#5cb0 .graf .graf--h4 .graf-after--li name="5cb0"}

Here's an example of using Sleuth Kit's tools to list and recover files
from unallocated space:

``` {#c4e1 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
# List deleted files in an NTFS image
fls -r -d /path/to/disk/image.img
```

``` {#ed5b .graf .graf--pre .graf-after--pre}
# Recover a file using its metadata address
icat /path/to/disk/image.img <metadata_address> > recovered_file
```

This process involves locating the file in the unallocated space and
using its metadata to reconstruct the file.
:::
::::
::::::

:::::: {#5b5b .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Method 5: Recovering from Backup or Shadow Copies {#925d .graf .graf--h3 .graf--leading name="925d"}

Sometimes, deleted files can be recovered from backups or shadow copies
(in Windows). Even if a file is deleted, it might still exist in a
previous version or a backup.

#### Steps to Recover from Backups {#8a4c .graf .graf--h4 .graf-after--p name="8a4c"}

1.  [**Access Backups:** Identify whether a backup exists for the time
    period when the file was still intact. This could be a local backup,
    cloud backup, or shadow copy.]{#1df8}
2.  [**Restore Files:** Use the backup software or system's built-in
    restore features to recover the file.]{#49cf}
3.  [**Verify Integrity:** Ensure the recovered file is intact and
    usable.]{#ba21}

#### Example: Using Windows Shadow Copies {#da6f .graf .graf--h4 .graf-after--li name="da6f"}

Windows Shadow Copies can be accessed to recover previous versions of
files.

``` {#df9a .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
vssadmin list shadows /for=C:
```

This command lists shadow copies available for the C: drive. You can use
tools like ShadowExplorer to browse and recover files from these copies.
:::
::::
::::::

:::::: {#e782 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Method 6: Advanced Recovery Using Forensic Tools {#b57d .graf .graf--h3 .graf--leading name="b57d"}

Forensic tools are designed for detailed analysis and recovery of
digital evidence, including deleted files. These tools provide more
advanced options for file recovery, allowing the user to work with a
wide range of file systems, formats, and scenarios.

#### Popular Forensic Tools {#46b0 .graf .graf--h4 .graf-after--p name="46b0"}

- [**EnCase:** A comprehensive forensic tool for recovering, analyzing,
  and preserving digital evidence.]{#e4a1}
- [**FTK (Forensic Toolkit):** Another powerful tool for data recovery
  and forensic analysis.]{#e314}
- [**X-Ways Forensics:** A streamlined and efficient forensic tool with
  advanced data recovery capabilities.]{#477c}

#### Example Using FTK Imager {#80a1 .graf .graf--h4 .graf-after--li name="80a1"}

FTK Imager allows you to create disk images and recover deleted files.
The following is a general process:

1.  [**Create a Disk Image:** Use FTK Imager to create a forensic image
    of the disk.]{#8d13}
2.  [**Mount the Image:** Mount the image in FTK Imager for
    analysis.]{#640e}
3.  [**Recover Files:** Browse through the file system and unallocated
    space to locate and recover deleted files.]{#7cf2}
:::
::::
::::::

:::::: {#6b74 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Preventive Measures: How to Securely Delete Files {#7ccd .graf .graf--h3 .graf--leading name="7ccd"}

While recovering deleted files is often possible, it's important to know
how to prevent unwanted recovery. Securely deleting files ensures that
they cannot be recovered even by advanced methods.

#### Steps to Securely Delete Files {#2f7e .graf .graf--h4 .graf-after--p name="2f7e"}

1.  [**Use File Shredding Software:** Tools like CCleaner, Eraser, or
    SDelete overwrite the data with random patterns, making recovery
    impossible.]{#a82e}
2.  [**Wipe Free Space:** Even after files are deleted, remnants might
    exist in free space. Tools like BleachBit can be used to securely
    wipe free space on a disk.]{#8ff8}
3.  [**Encrypt Sensitive Files:** Before deleting, consider encrypting
    sensitive files. Even if remnants are recovered, they will be
    unusable without the encryption key.]{#5220}

#### Example Using SDelete {#3a8f .graf .graf--h4 .graf-after--li name="3a8f"}

SDelete is a command-line tool from Sysinternals that securely deletes
files.

``` {#98bc .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
sdelete -p 3 -z C:
```

This command securely deletes files and cleans free space on the C:
drive using three passes of overwriting.
:::
::::
::::::

:::::: {#a6f7 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Conclusion {#cccf .graf .graf--h3 .graf--leading name="cccf"}

Recovering deleted files is a skill that ethical hackers, forensic
experts, and IT professionals often need to master. Whether you're
dealing with accidental deletions or analyzing a compromised system,
understanding these recovery techniques is crucial.

This blog covered various methods to recover deleted files, including
using data recovery software, file carving, file system analysis, and
more. While recovering files can be useful, it's equally important to
understand how to securely delete files to protect sensitive
information.

By mastering these techniques, you not only gain the ability to recover
lost data but also enhance your knowledge of how data is stored,
managed, and secured on digital systems.

### Promote and Collaborate on Cybersecurity Insights {#b0e7 .graf .graf--h3 .graf-after--p name="b0e7"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#334f .graf .graf--h3 .graf-after--p name="334f"}

[Vijay
Gupta](https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2"
rel="noopener" target="_blank"} is a cybersecurity enthusiast with
several years of experience in cyber security, [cyber crime forensics
investigation](https://play.google.com/store/books/details?id=VRz7EAAAQBAJ){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/details?id=VRz7EAAAQBAJ"
rel="noopener ugc nofollow noopener" target="_blank"}, and security
awareness training in schools and colleges. With a passion for
safeguarding digital environments and educating others about
cybersecurity best practices, Vijay has dedicated his career to
promoting cyber safety and resilience. Stay connected with Vijay Gupta
on various social media platforms and professional networks to access
valuable insights and stay updated on the latest cybersecurity trends.
:::
::::
::::::
:::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 4, 2024](https://medium.com/p/6639fc55549b).

[Canonical
link](https://medium.com/@bevijaygupta/ways-i-can-find-your-deleted-files-as-an-ethical-hacker-6639fc55549b){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
