# capstone
capstone project




Data Science Problem
	-  can we use text patterns to see large scale trends in the change in thinking over time? Can this technique be applied to political documents to illustrate trends or predict events?
		- look at Neg/Pos sentiment, Subj/Obj, and political lib/con
		- LIGHTLY outline postmodernism and what it means basically

Data Used
	- Sentiment
		- UCI combined sentiment
			- 3 datasets with differing lengths
	- Subjectivity
		- subj_obj 
	- Predictions
		- State of the Union Speeches
		- DOJ press releases
		- inaugural addresses
		- supreme court decisions

Methods
	- Data Acquisition
		- Web scraping with BeautSoup
		- rest are datasets
	- preprocessing
		- lowercase everything
		- strip non-alpha characters
		- tokenize at word level
		- create vocab bank
		- truncate / pad all documents to appropriate column length
	- modeling
		- LSTM recurrent neural networks
		- Accuracy scores analysis
		- build some confusion matrices?
	- Saving model and tokenizer for reusability with pickle
		- heroku hosted app demo

Conclusions
	- SOTU
	- Inagu
	- DOJ
	- COURT
	- Sent overview
	- Subjectivityu

Concerns
	- how has language changed over time?
	- how does data length affect predictions?
	- how can we assess ideology? Doesn't seem to be a link between political affil and what they are saying
		- is this commesurant? with change in subjectivity?