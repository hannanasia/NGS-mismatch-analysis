# NGS-mismatch-analysis
Computational detection and characterisation of nucleotide mismatches in S.pombe sequencing data to investigate mutation patterns in genotoxic agent-treated and -untreated samples. The purpose of this program is to investigate whether treatment is associated with increased mutation frequency and specific mismatch positions.
## How to Run the Program 
Open the notebook in Google Colab using File -> Open notebook -> Upload. Upload the .ipynb file, then select Runtime -> Run all to execute the analysis and display the results.
## Inputs and Outputs 
The program takes a reference DNA sequence and sequencing reads containing read IDs, sample names, treatment groups, and nucleotide sequences. It validates each read and identifies mismatches against the reference. It returns annotated reads, sample summaries, and statistical comparisons. The displayed results include valid and invalid read counts, mismatch percentages, substitution frequencies, the three most frequently mutated positions, and Welch's t-test results.
## Code Design 
I divided the analysis into separate functions so that each stage could be tested independently. For example, validate_read() checks sequence length and nucleotide characters before find_mutations() identifies mismatches. This prevents invalid reads from contributing to mutation counts.

I used dictionaries to store mutation information because they allow counts to be undated and accessed using positions or substitution types. For example position_counts stores mismatch frequencies by nucleotide position. An alternative was to use separate lists, but dictionaries made it easier to combine counts across samples.

I also sorted mismatch positions by descending frequency and the ascending position. This ensures that positions with equal counts are ranked consistently with the earlier position appearing first. Finally, samples with no valid reads are excluded from percentage calculations to avoid division by zero.
## Testing 
I used assert statements to check different situations first. First I tested known mismatches to verify that the correct positions and percentages were calculated. Second I tested empty inputs and samples with no mismatches to check that the functions handled these cases correctly. Third I tested samples with zero valid reads to ensure they were excluded from statistical comparisons without causing errors.
## Overall
The program uses separate functions to validate reads, identify mismatches, and compare treatment groups. For example, invalid reads are excluded to prevent inaccurate mutation counts, while mismatch positions are ranked by frequency to identify high mutation positions. Welch's t-test assesses whether differences between groups are statistically significant. The results for my data set showed significantly higher mismatch frequencies at positions 97-99 in treated samples, supporting how the investigation of how genotoxic treatment affects DNA mutation patterns in S.pombe.
