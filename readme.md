#DNA Data Storage
##Channel Coding for Mutation Resistance

What if historians today had access to detailed census data from hundreds or thousands of years ago? It's pretty obvious that our understanding of past cultures would be drastically different. However, what are we doing to prevent the same cycle hundreds of years from now? Where are we storing the massive reams of data that future societies would find invaluable?

The short answer is nowhere useful. It's stored on hard disks, or perhaps metallic platters, some of it tucked away in vaults, some of it not. Few of these storage mediums have adequate life spans. All of them demand resources in terms of space, power, maintenance etc. Even if these disks and platters survived for the next 500 years, there is no guarantee that future societies will have the capability to read these ancient forms of data.

What if we used DNA? An incredibly resilient organic molecule, it's no new idea that DNA is a storage medium ripe for exploration. However, an encoding scheme must be used that protects against the imperfections in DNA synthesis and sequencing, as well as natural degredation over time.

Proposed here is a small stab at a large problem, using Hamming Codes to encode binary data in nucleotides.

###Software

The included Python program can read any ASCII text file, and encode it in a DNA sequence that is aligned on 13 bits of data in a (13,8) Hamming Code. That is, 5 parity bits for every 8 bits of original data. The output is in FASTA format.

With an encoded file, the same program can be used to decode an encoded DNA sequence, in FASTA format, back to its original content.

The program makes use of the Python multiprocessing library.
###Included Files
* `convert.py`: Python script for encoding and decoding
* `resources/`: Several testing text files ranging from small to large sizes

###Usage
`convert.py` takes several command line arguments:

	usage: convert.py [-h] [--decode] [--encode] [--workers W] input [output]

	positional arguments:
		input
		output
		
	optional arguments:
		-h, --help         show this help message and exit
		--decode, -d       decode boolean flag
		--encode, -e       encode boolean flag
		--workers W, -w W  number of processes to spawn
		
**Only two arguments are required:**

*Specify encoding or decoding:*

* `--encode, -e`: Convert a text file into DNA, in FASTA format, encoded with (13,8) Hamming Code
* `--decode, -d`: Convert a FASTA file of 13 bit aligned DNA (same format as output of --encode) back to its original format.

*Specify input file*

* The first non-flag argument is the input text file. For `--encode`, this is a normal text file. For `--decode` this is a FASTA formatted Hamming encoded file.

**Optional arguments:**

* `-h, --help` : Get usage documentation
* `-w W` : Specify the number of processes (workers) to spawn to make use of multiple cores. Default is 1.
* output file: The second non-flag positional argument is the output destination. Default is `out.txt`.

###Dependencies
The following libraries are required for this software:

* bitstring: https://code.google.com/p/python-bitstring/
* bitarray: https://pypi.python.org/pypi/bitarray/
* binascii: https://docs.python.org/2/library/binascii.html
* multiprocessing