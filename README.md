"# accenture" 
trigger ClosedOpportunityTrigger on Opportunity(after insert, after update) {

	List<Task> taskRelated = new List<Task> ();

	for (Opportunity Opp :[select Id, Name, StageName FROM Opportunity where ID IN :Trigger.new]) {
		if (Opp.StageName == 'Closed Won') {
			taskRelated.add(new task(whatId = Opp.Id, Subject = 'Follow Up Test Task', Status = 'Not Started'));
		}
	}
	if (taskRelated.size() > 0)
	{
		Insert taskRelated; }



}
