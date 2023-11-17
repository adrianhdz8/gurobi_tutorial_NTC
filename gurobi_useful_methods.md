# Useful Methods and Parameters in Gurobi

Attributes in Gurobi can generally be set by:
```python
model.setAttr('attrName', <attrValue>)      # for model-specific attributes
var.setAttr('attrName', <attrValue>)        # for variable-specific attributes
constr.setAttr('attrName', <attrValue>)     # for constraint-specific attributes
```
and retrieved by:
```python
model.getAttr('attrName', <attrValue>)      # for model-specific attributes
  model.getAttr('x', <var>)                 # example method for retrieving model solution values for <var>
var.getAttr('attrName', <attrValue>)        # for variable-specific attributes
constr.getAttr('attrName', <attrValue>)     # for constraint-specific attributes
```


[LPWarmStart](https://www.gurobi.com/documentation/current/refman/lpwarmstart.html#parameter:LPWarmStart): set whether to use a warm start solution or bounds. It is specified using the attributes VBasis and CBasis or PStart and DStart on the original model.

[Start](https://www.gurobi.com/documentation/current/refman/start.html): pass a warm start to the MIP that has been built for initializing the solver at this solution. For example:
```python
model.setAttr('Start', <startValue>)
```

[MIPGap](https://www.gurobi.com/documentation/current/refman/mipgap2.html): set the desired solution tolerance for the MIP solver. Default is set at $10^{-4}$.

[NetworkAlg](https://www.gurobi.com/documentation/current/refman/networkalg.html#parameter:NetworkAlg): set whether to use network simplex to solve problem (default chooses automatically).

[InfUnbdInfo](https://www.gurobi.com/documentation/current/refman/infunbdinfo.html#parameter:InfUnbdInfo): (0 for no 1 for yes) set whether you want gurobi to compute additional information in the case the model is unbounded (computes the unbounded ray – see UnbdRay) or infeasible (computes the infeasibility proof – see FarkasDual and FarkasProof).

[UnbdRay](https://www.gurobi.com/documentation/current/refman/unbdray.html#attr:UnbdRay): provides vector of unbounded ray for problem (only when InfUnbdInfo set to 1). When added to any feasible solution, this yields a new solution that is also feasible and improves the objective.

[DualReductions](https://www.gurobi.com/documentation/current/refman/dualreductions.html#parameter:DualReductions): determines whether dual reductions are performed during optimization. Can be used to determine if the model was infeasible or unbounded.

[Status](https://www.gurobi.com/documentation/10.0/refman/status.html): (e.g., model.Status == GRB.OPTIMAL) optimization status of the model matching one of the [Status Codes](https://www.gurobi.com/documentation/10.0/refman/optimization_status_codes.html#sec:StatusCodes):
-	GRB.LOADED or 1: model loaded but noy yet solved.
-	GRB.OPTIMAL or 2: model solved to optimality.
-	GRB.INFEASIBLE or 3: model proven to be infeasible.
-	GRB.INF_OR_UNBD or 4: model proven to be either infeasible or unbounded. To obtain a more definitive conclusion, set the DualReductions parameter to 0 and reoptimize.
-	GRB.UNBOUNDED or 5: model proven to be unbounded (indicates the presence of an unbounded ray that allows the objective to improve without limit).

[Pi](https://www.gurobi.com/documentation/10.0/refman/pi.html): the constraint dual value in the current solution (a.k.a. shadow price).

[Slack](https://www.gurobi.com/documentation/10.0/refman/slack.html): constraint slack in the current solution.

[Write](https://www.gurobi.com/documentation/current/refman/py_model_write.html): write full Gurobi model to file. Can help debugging or writing out constraints for a given example.
