### Save generated figures on server (by command line execution)

```
import matplotlib.pyplot as plt
plt.switch_backend('agg')
# %matplotlib inline --> for jupyter notebook  

plt.figure(0, figsize=(8, 5))
plt.plot(fpr, tpr, lw=2, label= ': AUC = %0.4f' % roc_auc)  
## Figure settings
plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate', fontsize=12)
plt.ylabel('True Positive Rate', fontsize=12)
plt.title('Receiver Operating Characteristic (ROC)', y=1.04, fontsize=14)
plt.legend(loc="lower right", bbox_to_anchor=(1,0))  

plt.savefig(savefig_path, bbox_inches='tight', dpi=300)
plt.show()
```

Ref: https://stackoverflow.com/questions/4706451/how-to-save-a-figure-remotely-with-pylab/4706614#4706614
