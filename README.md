ARSON-Spec
==========

A Reasonably Small Object Notation
---------------------------------

*"It tastes like burning."*

<h3>Overview:</h3>
<p>ARSON is a binary data exchange format inspired by <a href="http://bsonspec.org">BSON</a>.</p>
			
<p>Like BSON, it creates a binary representation of JSON-like serialized data structures.  It is largely schemaless, which does make it less efficient than formats such as ProtocolBuffers.  This lack of efficiency is traded for an increased degree of flexibility and expressiveness.  Unlike BSON, ARSON is not designed to be a format for data storage, but rather one for rapid, transactional data streams. The intended use case for ARSON is one in which large volumes of arbitrary data structures must be transacted and parsed quickly. ARSON isn't designed to be prudent, or even particularly sane. It's designed for punting updates back and forth. Consider yourself notified.</p>
			
<p>ARSON's priorities are:</p>
<ul>
	<li><b>Efficiency:</b> It should be fast and efficient to transmit, encode, and decode.</li>
	<li><b>Flexibility:</b> It should be able to be utilized across a wide range of use cases and applications.</li>
	<li><b>Expressiveness:</b> It should exhibit JSON-like expressiveness, and provide facilities for specialization.</li>
	<li><b>Traversability:</b> It should be fast for a parser to traverse a unkown document and quickly ascertain it's properties.</li>
</ul>
			
<h3>Features:</h3>
			
<p>Here are some of the data types ARSON supports:</p>
<ul>
	<li>Embedded Documents</li>
	<li>Heterogenous and Typed Arrays</li>
	<li>Integers (16-64 bits)</li>
	<li>Floating Point (64 bit IEEE 754)</li>
	<li>Booleans</li>
	<li>Strings</li>
	<li>UUIDs, Hashes, and raw Binary</li>
	<li>Metadata Tags</li>
	<li>User-Defined Types</li>
</ul>
			
<p>One of the main oddities of ARSON is its use of nibbles rather than bytes as its primary unit of measurement. There is a 1 nibble type address space, and length measurements are by and large expressed in terms of nibbles. This may appear to be an odd choice, but was done so to streamline the format in terms of byte efficiency and to enforce smaller document sizes.  Given the intent of ARSON to be a format optimized for streaming, these are worthy goals. The maximum size of a ARSON document is roughly 32kB.</p>
			
<p>ARSON introduces several concepts not found within BSON and removes many implementation-specific types found within BSON.  The end result is hopefully a format which more expressive and less anchored to a specific application. </p>
			
<p>ARSON has a specific type for User-defined Types. It provides facilities for an application to express up to 16 arbitrary types. This is designed for efficiency at the cost of universal parseability. For instance, it allows a 3D application to define a compact representation for Vectors, or Rotations that abstains from the usual key:value semantics. In addition to a subtype specifier, UserTypes also contain a length value which maintains the parseability of the larger data structure. Given the flexibility and potential ambiguity UserTypes provide, it's prudent to ignore UserType values found in the wild unless their subtypes are definitively known. </p>
			
<p>ARSON also includes a type for Document Metadata Tags.  This is a feature often cited as a shortcoming of JSON, and it is provided here as an experiment into what can be done with it. One potential application for this is XML-ish style extensibility with embedded documents acting as nested tags. Rigid schema batteries not included, may pose choking risk to small children, Anarchy in the UK.  For a proposed schema, check out AXE.</p>
