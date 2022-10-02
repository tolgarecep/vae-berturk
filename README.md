## datasets
**text categorization (dünya, ekonomi, sağlık, spor, kültür, siyaset, teknoloji)**: 3430, 1470; 700x7  
**sentiment analysis (neg, pos)**: 6000, 2489; 4252+4237  
**sentiment analysis (neu, neg, pos)**: 5000, 1000; 2715+1698+587  
**ticaret**: 5000, 1000; 6x1000

## training comparison
| vae training | text categorization (7) | sentiment analysis (binary) | sentiment analysis (neu, neg, pos) | text categorization (6)
| ------------- | ------------- | ------------- | ------------- | ------------- |
| 180K, 6 epochs | 0.4496598639455782 | 0.6753716351948573 | 0.858 | 0.573 |
| 360K, 3 epochs | 0.563265306122449 | 0.6894335074327039 | 0.866 | 0.637 |
| 1080K, 1 epoch | 0.42585034013605444 | 0.6801928485335476 | 0.856 | 0.454 |
| 4320K, 1 epoch | X | X | X | X |

## dim_z comparison
vae training: 360/3
| model/method | text categorization (7) | sentiment analysis (binary) | sentiment analysis (neu, neg, pos) | text categorization (6)
| ------------- | ------------- | ------------- | ------------- | ------------- |
| vae `dim_z=64` | 0.5571428571428572 | 0.685415829650462 | 0.8646666666666667 | 0.657 |
| vae `dim_z=128` | 0.563265306122449 | 0.6894335074327039 | 0.866 | 0.637 | 
| vae `dim_z=256` | 0.4530612244897959 | 0.6838087585375653 | 0.8586666666666666 | 0.59 | 
| berturk | 0.8625850340136054 | 0.8782643631980716 | 0.9333333333333333 | 0.9130000000000001 |
| tf-idf | 0.9108843537414966 `dim_z=46389` | 0.9023704298915227 `dim_z=8792` | 0.882 `dim_z=8119`| 0.954 `dim_z=14190` |
