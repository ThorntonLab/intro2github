#Organization of a project on HPC

You have 3 folders:
1.  scripts/:  this is a git repo that you have cloned from another source.
2.  data/: this contains your data for analysis.  Typically, this data will have been copied from another source.
3.  output/: your scripts analyze data and write output here

As you modify files in scripts/, you may push those changes back to the home repo (be it on github or another server at UCI).

With the above layout, all of your "data processing" stuff is restricted to the scripts/ folder and _is backed up_ to the home repo.

The data are already "backed up" because they came from elsewhere.

output/ may not need to be backed up, although it could be if it is small.  Rather, you should be able to recreate everything in output in the event of an HPC disaster by re-cloning your scriptss/ repo, repopulating data/, and then re-running the workflow

#Pro tips

1.  scripts/ may want to contain scripts to populate data/.  For example, the rsync or wget commands needed to get the data from their source
3.  You may want a fourth folder, perhaps called SImaterial/, which contains small-to-medium sized plain text files that come from output/.  For example, FPKM per gene/transcript from an RNA-seq analysis, etc.  These files are likely to be SI data.  You can make SImaterial/ a repo, too.