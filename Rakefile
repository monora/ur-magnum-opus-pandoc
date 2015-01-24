require "rake/clean"

ODTTMPL = "Template/ODT/odt-template.txt"
ODTREF  = "Template/ODT/reference.odt"

# Define inputs and outputs
MDFILES = FileList["**/*.md"]
PDFS = MDFILES.ext(".pdf")
DOCX = MDFILES.ext(".docx")
ODTS = MDFILES.ext(".odt")

# Clobber only PDFs and DOCXs we've generated
CLOBBER.include(PDFS, DOCX, ODTS)

# Define bibliography and CSL files
BIB = "Quellen/Quellen.bib"
CSL = "Template/CSL/ur-magnum-opus-zotero.csl"

desc "Build all documents in all formats."
task :default => [:pdfs, :docx, :odts]

desc "Build PDFs of all documents."
task :pdfs => PDFS

desc "Build DOCXs of all documents."
task :docx => DOCX

desc "Build ODTs of all documents."
task :odts => ODTS

# Build PDFs from Markdown source
rule ".pdf" => ".md" do |t|
  sh "pandoc #{t.source} -o #{t.name} --csl=#{CSL} --bibliography=#{BIB}"
end

# Build HTMLs from Markdown source
rule ".html" => ".md" do |t|
  sh "pandoc #{t.source} -o #{t.name} --csl=#{CSL} --bibliography=#{BIB}"
end

# Build ODTs from Markdown source
rule ".odt" => ".md" do |t|
  pandoc t,
	       "--smart",
         "--template=#{ODTTMPL}", "--reference-odt=#{ODTREF}"
end

# Build DOCXs from Markdown source
rule ".docx" => ".md" do |t|
  pandoc t
end

def pandoc(t, *args)
  sh "pandoc",  t.source, '-o', t.name, "--csl=#{CSL}", "--bibliography=#{BIB}", *args
end
