cmake_minimum_required(VERSION 3.10)
project(CV_Resume NONE)

# Set LaTeX compiler
set(LATEX_COMPILER pdflatex)

# Set the main LaTeX file
set(MAIN_TEX_FILE main.tex)
set(OUTPUT_PDF_FILE main.pdf)

# Find LaTeX
find_program(LATEX_EXECUTABLE ${LATEX_COMPILER})
if(NOT LATEX_EXECUTABLE)
    message(WARNING "LaTeX compiler '${LATEX_COMPILER}' not found. Please install a LaTeX distribution like MiKTeX or TeX Live.")
    message(STATUS "You can download MiKTeX from: https://miktex.org/download")
    message(STATUS "Or use the compile.bat file once LaTeX is installed.")
else()
    message(STATUS "LaTeX compiler found: ${LATEX_EXECUTABLE}")
endif()

# Custom command to compile LaTeX to PDF
add_custom_command(
    OUTPUT ${OUTPUT_PDF_FILE}
    COMMAND ${LATEX_EXECUTABLE} -interaction=nonstopmode -file-line-error ${MAIN_TEX_FILE}
    COMMAND ${LATEX_EXECUTABLE} -interaction=nonstopmode -file-line-error ${MAIN_TEX_FILE}
    DEPENDS ${MAIN_TEX_FILE}
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    COMMENT "Compiling LaTeX document to PDF"
    VERBATIM
)

# Custom target for building the PDF
add_custom_target(
    pdf
    DEPENDS ${OUTPUT_PDF_FILE}
    COMMENT "Building PDF from LaTeX source"
)

# Set the default target
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY DEFAULT_TARGET pdf)

# Clean target to remove generated files
add_custom_target(
    clean-latex
    COMMAND ${CMAKE_COMMAND} -E remove -f *.aux *.log *.out *.toc *.bbl *.blg *.idx *.ind *.ilg *.lof *.lot *.fdb_latexmk *.fls *.synctex.gz *.nav *.snm *.vrb
    COMMENT "Cleaning LaTeX auxiliary files"
)

# Print configuration info
message(STATUS "Main LaTeX file: ${MAIN_TEX_FILE}")
message(STATUS "Output PDF file: ${OUTPUT_PDF_FILE}")
message(STATUS "")
message(STATUS "To build the PDF, run: cmake --build . --target pdf")
message(STATUS "To clean auxiliary files, run: cmake --build . --target clean-latex")
