[![Build Status](https://travis-ci.org/swiftonfile/swiftonfile.svg?branch=master)](https://travis-ci.org/swiftonfile/swiftonfile)

# Swift-on-File
Swift-on-File is a Swift Object Server implementation that enables users to
access the same data, both as an object and as a file. Data can be stored and
retrieved through Swift's REST interface or as files from NAS interfaces 
including native GlusterFS, NFS and CIFS.

Swift-on-File is to be deployed as a Swift [storage policy](http://docs.openstack.org/developer/swift/overview_policies.html),
which provides the advantages of being able to extend an existing Swift cluster
and also migrating data to and from policies with different storage backends.

The main difference from the default Swift Object Server is that Swift-on-File
stores objects following the same path hierarchy as the object's URL. In contrast,
the default Swift implementation stores the object following the mapping given
by the Ring, and its final file path is unkown to the user.

For example, an object with URL: `https://swift.example.com/v1/acct/cont/obj`,
would be stored the following way by the two systems:
* Swift: `/mnt/sdb1/2/node/sdb2/objects/981/f79/f566bd022b9285b05e665fd7b843bf79/1401254393.89313.data`
* SoF: `/mnt/swiftonfile/acct/cont/obj`

## Use cases
Swift-on-File can be especially useful in cases where access over multiple
protocols is desired. For example, imagine a deployment where video files
are uploaded as objects over Swift's REST interface and a legacy video transcoding
software access those videos as files.

Another use case is where users might need to migrate data from an existing file
storage systems to a Swift cluster.

## Limitations and Future plans
Swift-On-File currently works only with Filesystems with extended attributes
support. It is also recommended that these Filesystems provide data durability
as Swift-On-File should not use Swift's replication mechanisms. 

GlusterFS is a good example of a Filesystem that works well with Swift-on-File,
GlusterFS provides a posix interface, global namespace, scalability, data
replication and support for extended attributes.

Currently, files added over a NAS protocol (e.g., native GlusterFS), do not show
up in container listings, still those files would be accessible over Swift's REST
interface with a GET request. We are working to provide a solution to this limitation.

Future plans includes adding support for Filesystems without extended attributes,
which should extend the ability to migrate data for legacy storage systems.
 
## Get involved:
To learn more about Swift-On-File, you can watch this presentation given at 
the Atlanta Openstack Summit: [Breaking the Mold with Openstack Swift and GlusterFS](http://youtu.be/pSWdzjA8WuA).
Presentation slides can be found [here](http://lpabon.github.io/openstack-summit-2014).

Join us in contributing to the project. Feel free to file bugs, help with documentation
or work directly on the code. You can communicate with us using GitHub [issues](https://github.com/swiftonfile/swiftonfile/issues) or find
us in the #swiftonfile channel on Freenode.

# Guides to get started:
1. [Quick Start Guide with XFS/GlusterFS](doc/markdown/quick_start_guide.md)
1. [Developer Guide](doc/markdown/dev_guide.md)
