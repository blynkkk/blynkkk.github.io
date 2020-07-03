# Change float to double \(\#41\)@b1f1a43

[Permalink](change-float-to-double-41-b1f1a43.md)

 Showing with **2 additions** and **2 deletions**.

1.  +2 −2 [new/en/datastream\_datatype.md](change-float-to-double-41-b1f1a43.md#diff-d66679912b8da08f2b80ec11fa273d90)

|  | @@ -7,14 +7,14 @@ Make sure you choose a correct Data Type for your data. Currently, these Data Ty |  |
| :--- | :--- | :--- |
|  |  |  \| Type \| Min \| Max \| |
|  |  |  \|:--------------:\|:---------------------------:\|:----------------------------:\| |
|  |  |  \| \`\`\`Integer\`\`\` \| -2,147,483,648 \| 2,147,483,647 \| |
|  |  |  \| \`\`\`Float\`\`\` \| -1.8 x 10^300 \| 4.9 x 10^-324 \| |
|  |  |  \| \`\`\`Double\`\`\` \| -1.8 x 10^300 \| 4.9 x 10^-324 \| |
|  |  |  \| \`\`\`String\`\`\` \| any value is accepted \| |
|  |  |  |
|  |  |  |
|  |  |  \*\*IMPORTANT:\*\* |
|  |  |  |
|  |  |  Blynk server will ignore values that don't match the Data Type |
|  |  |  |
|  |  |  Example: if Datastream has Data Type set to \`\`\`Integer\`\`\`, but Hardware sends \`\`\`123.45\`\`\`, this value will be skipped because it is \`\`\`Float\`\`\`, not \`\`\`Integer\`\`\`. |
|  |  |  Example: if Datastream has Data Type set to \`\`\`Integer\`\`\`, but Hardware sends \`\`\`123.45\`\`\`, this value will be skipped because it is \`\`\`Double\`\`\`, not \`\`\`Integer\`\`\`. |
|  |  |  |
|  |  |  If the incoming value goes out of range of Min or Max setting, this value will be "cropped" to match this setting. |

