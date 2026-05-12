import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the restaurant profile dataset
df_profiles = pd.read_csv(r"C:\Users\Keshav\Downloads\zippyeats restaurant profiles.csv")

# Set the visual style
sns.set_theme(style="whitegrid")
plt.figure(figsize=(12, 7))

# Create a scatter plot
# Color-coding by 'is_active' helps show that churn (status 0)
# happens regardless of follower count.
plot = sns.scatterplot(
    data=df_profiles,
    x='social_media_followers',
    y='cancellation_rate_pct',
    hue='is_active',
    palette='Set1',
    s=100,
    alpha=0.7
)

# Add a regression line (without scatter) to show the "flat" correlation
sns.regplot(
    data=df_profiles,
    x='social_media_followers',
    y='cancellation_rate_pct',
    scatter=False,
    color='black',
    line_kws={"linestyle": "--", "linewidth": 1.5}
)

# Labeling and Formatting
plt.title('Dead End Analysis: Social Media Followers vs. Cancellation Rates', fontsize=15)
plt.xlabel('Social Media Followers (Instagram + Facebook)', fontsize=12)
plt.ylabel('Cancellation Rate (%)', fontsize=12)
plt.legend(title='Partner Status', labels=['Inactive (Churned)', 'Active'])

# Annotate specific outliers to drive the point home for the CEO
# Example: Ginger Point (R016) has 6,231 followers but is inactive
plt.annotate('High Follower / High Cancel (Inactive)', xy=(6231, 5.3), xytext=(4500, 15),
             arrowprops=dict(facecolor='black', shrink=0.05, width=1))

plt.tight_layout()
plt.show()
