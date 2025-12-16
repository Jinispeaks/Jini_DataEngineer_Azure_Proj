Recently, I started using the 𝗤𝗨𝗔𝗟𝗜𝗙𝗬 clause in Databricks SQL, and it helped reduce unnecessary CTEs when filtering on window functions.

𝗧𝘆𝗽𝗶𝗰𝗮𝗹 𝗮𝗽𝗽𝗿𝗼𝗮𝗰𝗵 (𝘄𝗶𝘁𝗵𝗼𝘂𝘁 𝗤𝗨𝗔𝗟𝗜𝗙𝗬):

𝚆𝙸𝚃𝙷 𝚛𝚊𝚗𝚔𝚎𝚍_𝚎𝚟𝚎𝚗𝚝𝚜 𝙰𝚂 (
 𝚂𝙴𝙻𝙴𝙲𝚃
 𝚞𝚜𝚎𝚛_𝚒𝚍,
 𝚎𝚟𝚎𝚗𝚝_𝚝𝚒𝚖𝚎,
 𝚁𝙾𝚆_𝙽𝚄𝙼𝙱𝙴𝚁() 𝙾𝚅𝙴𝚁 (
 𝙿𝙰𝚁𝚃𝙸𝚃𝙸𝙾𝙽 𝙱𝚈 𝚞𝚜𝚎𝚛_𝚒𝚍
 𝙾𝚁𝙳𝙴𝚁 𝙱𝚈 𝚎𝚟𝚎𝚗𝚝_𝚝𝚒𝚖𝚎 𝙳𝙴𝚂𝙲
 ) 𝙰𝚂 𝚛𝚗
 𝙵𝚁𝙾𝙼 𝚎𝚟𝚎𝚗𝚝𝚜
)
𝚂𝙴𝙻𝙴𝙲𝚃 *
𝙵𝚁𝙾𝙼 𝚛𝚊𝚗𝚔𝚎𝚍_𝚎𝚟𝚎𝚗𝚝𝚜
𝚆𝙷𝙴𝚁𝙴 𝚛𝚗 = 𝟷;


The CTE here exists only to apply a filter.

𝗨𝘀𝗶𝗻𝗴 𝗤𝗨𝗔𝗟𝗜𝗙𝗬:

𝚂𝙴𝙻𝙴𝙲𝚃
 𝚞𝚜𝚎𝚛_𝚒𝚍,
 𝚎𝚟𝚎𝚗𝚝_𝚝𝚒𝚖𝚎
𝙵𝚁𝙾𝙼 𝚎𝚟𝚎𝚗𝚝𝚜
𝚀𝚄𝙰𝙻𝙸𝙵𝚈 𝚁𝙾𝚆_𝙽𝚄𝙼𝙱𝙴𝚁() 𝙾𝚅𝙴𝚁 (
 𝙿𝙰𝚁𝚃𝙸𝚃𝙸𝙾𝙽 𝙱𝚈 𝚞𝚜𝚎𝚛_𝚒𝚍
 𝙾𝚁𝙳𝙴𝚁 𝙱𝚈 𝚎𝚟𝚎𝚗𝚝_𝚝𝚒𝚖𝚎 𝙳𝙴𝚂𝙲
) = 𝟷;


Why QUALIFY is useful:

• Filters results after window functions are evaluated
• Eliminates extra CTEs and subqueries
• Makes SQL easier to read and maintain
• Very helpful for deduplication and “latest record per key” patterns

𝗡𝗼𝘁𝗲: QUALIFY works with window functions only and is supported in Databricks SQL (and a few other engines).

Small SQL features like this can significantly improve query clarity in analytics pipelines.
