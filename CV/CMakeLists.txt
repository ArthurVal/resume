cmake_minimum_required(VERSION 3.11)

project(CV_Arthur_Valiente
  VERSION 0.1.0
  DESCRIPTION "My CV")

include(CMakePrintHelpers)

find_package(LATEX COMPONENTS PDFLATEX REQUIRED)
# LATEX_FOUND: whether found Latex and requested components
# LATEX_<component>_FOUND: whether found <component>
# LATEX_COMPILER: path to the LaTeX compiler
# PDFLATEX_COMPILER: path to the PdfLaTeX compiler
# XELATEX_COMPILER: path to the XeLaTeX compiler
# LUALATEX_COMPILER: path to the LuaLaTeX compiler
# BIBTEX_COMPILER: path to the BibTeX compiler
# BIBER_COMPILER: path to the Biber compiler
# MAKEINDEX_COMPILER: path to the MakeIndex compiler
# XINDY_COMPILER: path to the xindy compiler
# DVIPS_CONVERTER: path to the DVIPS converter
# DVIPDF_CONVERTER: path to the DVIPDF converter
# PS2PDF_CONVERTER: path to the PS2PDF converter
# PDFTOPS_CONVERTER: path to the pdftops converter
# LATEX2HTML_CONVERTER: path to the LaTeX2Html converter
# HTLATEX_COMPILER: path to the htlatex compiler

cmake_print_variables(LATEX_COMPILER)
cmake_print_variables(PDFLATEX_COMPILER)

add_custom_command(
    OUTPUT ${PROJECT_NAME}_FR.pdf
    COMMAND TEXINPUTS=${CMAKE_CURRENT_SOURCE_DIR}:${CMAKE_CURRENT_SOURCE_DIR}/FortySecondsCV//: ${PDFLATEX_COMPILER} -output-directory ${CMAKE_CURRENT_BINARY_DIR} -jobname ${PROJECT_NAME}_FR -interaction=nonstopmode ${CMAKE_CURRENT_SOURCE_DIR}/main.tex
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/main.tex
    VERBATIM)

add_custom_target(${PROJECT_NAME}_FR ALL DEPENDS ${PROJECT_NAME}_FR.pdf)
